<template>
  <section
    id="hero"
    class="relative min-h-screen flex items-center justify-center bg-black overflow-hidden"
  >
    <!-- background grid -->
    <div
      class="absolute inset-0 bg-[linear-gradient(rgba(255,255,255,0.03)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.03)_1px,transparent_1px)] bg-size-[72px_72px]"
    ></div>
    <!-- glow -->
    <div
      class="absolute top-1/3 left-1/2 -translate-x-1/2 -translate-y-1/2 w-150 h-150 bg-violet-600/20 rounded-full blur-[120px] pointer-events-none"
    ></div>

    <div class="relative z-10 text-center max-w-3xl px-6">
      <!-- badge -->
      <div
        class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full border border-violet-500/40 bg-violet-500/10 text-violet-300 text-xs tracking-widest uppercase mb-8"
      >
        <span
          class="w-1.5 h-1.5 rounded-full bg-violet-400 animate-pulse"
        ></span>
        Available for work
      </div>

      <h1
        class="text-6xl md:text-7xl font-bold text-white leading-tight mb-4 tracking-tight"
      >
        Hi, I'm
        <span
          class="bg-linear-to-r from-violet-400 to-pink-400 bg-clip-text text-transparent"
          >Nick</span
        >
      </h1>

      <!-- typewriter -->
      <div class="h-10 flex items-center justify-center mb-6">
        <span class="text-2xl md:text-3xl font-semibold text-white/70">
          {{ displayedText
          }}<span class="animate-blink text-violet-400">|</span>
        </span>
      </div>

      <p class="text-xl text-white/50 mb-10 leading-relaxed max-w-xl mx-auto">
        中原大學資管所碩士，熱愛網頁開發與機器學習，喜歡用程式碼解決真實問題。
      </p>

      <div class="flex gap-4 justify-center flex-wrap">
        <a
          href="#projects"
          class="px-8 py-3.5 bg-white text-black rounded-full font-semibold hover:bg-white/90 transition-all duration-300 hover:scale-105"
        >
          查看作品
        </a>
        <a
          href="#contact"
          class="px-8 py-3.5 border border-white/20 text-white rounded-full font-semibold hover:border-white/50 hover:bg-white/5 transition-all duration-300"
        >
          聯絡我
        </a>
      </div>

      <!-- scroll hint -->
      <div
        class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 text-white/30 text-xs tracking-widest uppercase"
      >
        <span>Scroll</span>
        <div
          class="w-px h-10 bg-linear-to-b from-white/30 to-transparent"
        ></div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const roles = ["Full-Stack Developer", "ML Engineer"];

const displayedText = ref("");
let roleIndex = 0;
let charIndex = 0;
let isDeleting = false;
let timer = null;

function tick() {
  const current = roles[roleIndex];

  if (!isDeleting) {
    displayedText.value = current.slice(0, charIndex + 1);
    charIndex++;
    if (charIndex === current.length) {
      isDeleting = true;
      timer = setTimeout(tick, 2000);
      return;
    }
    timer = setTimeout(tick, 80);
  } else {
    displayedText.value = current.slice(0, charIndex - 1);
    charIndex--;
    if (charIndex === 0) {
      isDeleting = false;
      roleIndex = (roleIndex + 1) % roles.length;
      timer = setTimeout(tick, 400);
      return;
    }
    timer = setTimeout(tick, 40);
  }
}

onMounted(() => {
  timer = setTimeout(tick, 600);
});
onUnmounted(() => clearTimeout(timer));
</script>

<style scoped>
@keyframes blink {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}
.animate-blink {
  animation: blink 0.8s step-end infinite;
}
</style>
