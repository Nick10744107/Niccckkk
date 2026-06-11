<template>
  <div class="pixel-box bg-ink p-2 sm:p-3 select-none">
    <!-- screen title bar -->
    <div
      class="flex items-center justify-between font-pixel text-phosphor text-xs sm:text-sm px-1 pb-2"
    >
      <span>NIBBLES.EXE</span>
      <span>SCORE {{ String(score).padStart(4, "0") }}</span>
    </div>

    <div class="relative">
      <canvas
        ref="canvas"
        :width="COLS * CELL"
        :height="ROWS * CELL"
        class="block w-full bg-crt [image-rendering:pixelated] outline-none focus-visible:ring-2 focus-visible:ring-phosphor"
        tabindex="0"
        role="application"
        aria-label="貪食蛇小遊戲,點擊後用方向鍵操控"
        @keydown="onKeydown"
        @click="takeControl"
      ></canvas>

      <!-- CRT scanlines + vignette -->
      <div
        class="absolute inset-0 pointer-events-none bg-[repeating-linear-gradient(0deg,rgba(0,0,0,0.28)_0px,rgba(0,0,0,0.28)_1px,transparent_1px,transparent_3px)]"
        aria-hidden="true"
      ></div>
      <div
        class="absolute inset-0 pointer-events-none bg-[radial-gradient(ellipse_at_center,transparent_55%,rgba(0,0,0,0.45)_100%)]"
        aria-hidden="true"
      ></div>

      <!-- overlay -->
      <div
        v-if="overlay"
        class="absolute inset-0 flex flex-col items-center justify-center gap-2 bg-crt/80 text-center"
      >
        <p class="font-pixel text-phosphor text-base sm:text-xl animate-blink-px">
          {{ overlay }}
        </p>
      </div>
    </div>

    <p class="font-pixel text-phosphor/50 text-xs px-1 pt-2">
      {{ mode === "play" ? "方向鍵操控 · 吃紅蘋果" : "點擊螢幕接手操控" }}
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const COLS = 24;
const ROWS = 14;
const CELL = 12;
const TICK_MS = 110;

const canvas = ref(null);
const score = ref(0);
const mode = ref("demo"); // demo | play | over
const overlay = ref("");

let ctx = null;
let snake = [];
let dir = { x: 1, y: 0 };
let nextDir = { x: 1, y: 0 };
let food = { x: 18, y: 7 };
let timer = null;
let overTimer = null;

function reset() {
  snake = [
    { x: 8, y: 7 },
    { x: 7, y: 7 },
    { x: 6, y: 7 },
  ];
  dir = { x: 1, y: 0 };
  nextDir = { x: 1, y: 0 };
  score.value = 0;
  spawnFood();
}

function spawnFood() {
  do {
    food = {
      x: Math.floor(Math.random() * COLS),
      y: Math.floor(Math.random() * ROWS),
    };
  } while (snake.some((s) => s.x === food.x && s.y === food.y));
}

function cellSafe(x, y) {
  if (x < 0 || y < 0 || x >= COLS || y >= ROWS) return false;
  return !snake.some((s) => s.x === x && s.y === y);
}

// demo 模式的簡單 AI:朝食物走,但優先避開牆和自己
function demoThink() {
  const head = snake[0];
  const candidates = [
    { x: Math.sign(food.x - head.x), y: 0 },
    { x: 0, y: Math.sign(food.y - head.y) },
    { x: 1, y: 0 },
    { x: -1, y: 0 },
    { x: 0, y: 1 },
    { x: 0, y: -1 },
  ].filter(
    (d) =>
      (d.x !== 0 || d.y !== 0) &&
      !(d.x === -dir.x && d.y === -dir.y) &&
      cellSafe(head.x + d.x, head.y + d.y)
  );
  if (candidates.length) nextDir = candidates[0];
}

function tick() {
  if (mode.value === "demo") demoThink();
  dir = nextDir;
  const head = { x: snake[0].x + dir.x, y: snake[0].y + dir.y };

  if (!cellSafe(head.x, head.y)) {
    if (mode.value === "play") {
      mode.value = "over";
      overlay.value = "GAME OVER — 按任意鍵再來";
    } else {
      reset();
    }
    return;
  }

  snake.unshift(head);
  if (head.x === food.x && head.y === food.y) {
    score.value += 10;
    spawnFood();
  } else {
    snake.pop();
  }
  draw();
}

function draw() {
  if (!ctx) return;
  ctx.fillStyle = "#071a2e";
  ctx.fillRect(0, 0, COLS * CELL, ROWS * CELL);

  // food(蘋果紅)
  ctx.fillStyle = "#e5484d";
  ctx.fillRect(food.x * CELL + 1, food.y * CELL + 1, CELL - 2, CELL - 2);

  // snake(亮青藍,頭部最亮)
  snake.forEach((s, i) => {
    ctx.fillStyle = i === 0 ? "#aee0ff" : "#54c2ff";
    ctx.fillRect(s.x * CELL + 1, s.y * CELL + 1, CELL - 2, CELL - 2);
  });
}

const KEY_DIRS = {
  ArrowUp: { x: 0, y: -1 },
  ArrowDown: { x: 0, y: 1 },
  ArrowLeft: { x: -1, y: 0 },
  ArrowRight: { x: 1, y: 0 },
  w: { x: 0, y: -1 },
  s: { x: 0, y: 1 },
  a: { x: -1, y: 0 },
  d: { x: 1, y: 0 },
};

function onKeydown(e) {
  if (mode.value === "over") {
    reset();
    mode.value = "play";
    overlay.value = "";
    e.preventDefault();
    return;
  }
  const d = KEY_DIRS[e.key];
  if (!d) return;
  e.preventDefault();
  if (mode.value !== "play") takeControl();
  if (d.x === -dir.x && d.y === -dir.y) return; // 不能直接回頭
  nextDir = d;
}

function takeControl() {
  canvas.value?.focus();
  if (mode.value === "demo" || mode.value === "over") {
    if (mode.value === "over") reset();
    mode.value = "play";
    overlay.value = "";
  }
}

onMounted(() => {
  ctx = canvas.value.getContext("2d");
  reset();
  draw();

  const reduced = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  if (reduced) {
    overlay.value = "PRESS START";
    // 等使用者主動操作才開始跑
    const start = () => {
      overlay.value = "";
      mode.value = "play";
      timer = setInterval(tick, TICK_MS);
      canvas.value?.removeEventListener("click", start);
    };
    canvas.value.addEventListener("click", start);
    return;
  }
  timer = setInterval(tick, TICK_MS);
});

onUnmounted(() => {
  clearInterval(timer);
  clearTimeout(overTimer);
});
</script>
