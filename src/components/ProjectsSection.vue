<template>
  <section id="projects" class="py-28 px-6 bg-white border-y-2 border-ink">
    <div class="max-w-5xl mx-auto">
      <!-- heading -->
      <div class="mb-14" data-reveal>
        <p class="font-pixel text-snake text-sm mb-3">▸ SELECT GAME</p>
        <h2 class="font-pixel text-4xl text-ink">精選作品</h2>
      </div>

      <!-- cartridges -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <a
          v-for="(project, i) in projects"
          :key="project.title"
          :href="project.demo || project.github"
          target="_blank"
          rel="noopener noreferrer"
          class="group pixel-box bg-shell block hover:-translate-x-0.5 hover:-translate-y-0.5 hover:shadow-[6px_6px_0_0_#0b2440] transition-all duration-150"
          data-reveal
          :style="{ animationDelay: `${i * 80}ms` }"
        >
          <!-- cartridge label strip -->
          <div
            class="h-3 border-b-2 border-ink"
            :class="i % 2 === 0 ? 'bg-snake' : 'bg-apple'"
          ></div>

          <div class="p-6">
            <div class="flex items-start justify-between mb-4">
              <span
                class="inline-flex w-12 h-12 items-center justify-center text-2xl bg-white border-2 border-ink"
                >{{ project.icon }}</span
              >
              <span class="font-pixel text-xs text-ink/40"
                >CART.{{ String(i + 1).padStart(2, "0") }}</span
              >
            </div>

            <h3 class="font-pixel text-xl text-ink mb-2">
              {{ project.title }}
            </h3>
            <p class="text-sm text-ink/60 leading-relaxed mb-5">
              {{ project.description }}
            </p>

            <div class="flex flex-wrap gap-2 mb-6">
              <span
                v-for="tag in project.tags"
                :key="tag"
                class="font-pixel text-xs px-2 py-1 bg-white border-2 border-ink text-ink"
                >{{ tag }}</span
              >
            </div>

            <div
              class="font-pixel text-sm text-ink/50 group-hover:text-snake transition-colors duration-150"
            >
              <span v-if="project.demo">▸ PLAY DEMO</span>
              <span v-else>▸ GITHUB</span>
            </div>
          </div>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
const projects = [
  {
    icon: "🐍",
    title: "Nibbles 貪食蛇",
    description:
      "以純 JavaScript 打造的經典貪食蛇遊戲,包含碰撞偵測、分數計算與鍵盤操控邏輯。首頁那台就是它的精神續作。",
    tags: ["JavaScript", "HTML", "CSS"],
    github: "https://github.com/Nick10744107/Nibbles",
    demo: "https://nick10744107.github.io/Nibbles/",
  },
  {
    icon: "♟️",
    title: "圍棋資訊網",
    description:
      "圍棋知識與資訊平台,涵蓋歷史演進、基本術語,並整合韓、日、中、台四大棋院資源連結。",
    tags: ["HTML", "CSS"],
    github: "https://github.com/Nick10744107/new-resume",
    demo: "https://nick10744107.github.io/new-resume/project1/index.html",
  },
  {
    icon: "🗾",
    title: "日本旅遊推薦網站",
    description:
      "日本旅遊規劃平台,介紹北海道、京都、富士山等熱門景點,並提供行程預約與會員功能。",
    tags: ["HTML", "CSS"],
    github: "https://github.com/Nick10744107/new-resume",
    demo: "https://nick10744107.github.io/new-resume/project2/index.html",
  },
  {
    icon: "🗺️",
    title: "Landmarks iOS App",
    description:
      "使用 Swift + SwiftUI 開發的 iOS 景點導覽應用程式,實作地圖整合與收藏功能。",
    tags: ["Swift", "SwiftUI", "iOS"],
    github: "https://github.com/Nick10744107/Landmarks",
  },
];
</script>
