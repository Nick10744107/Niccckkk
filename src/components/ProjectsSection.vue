<template>
  <section id="projects" class="py-32 px-6 bg-neutral-950">
    <div class="max-w-6xl mx-auto">
      <!-- heading -->
      <div class="mb-16">
        <p class="text-violet-400 text-xs tracking-widest uppercase mb-3">
          Portfolio
        </p>
        <h2 class="text-4xl font-bold text-white">精選作品</h2>
      </div>

      <!-- cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <a
          v-for="project in projects"
          :key="project.title"
          :href="project.demo || project.github"
          target="_blank"
          class="group relative bg-white/5 border border-white/10 rounded-2xl p-7 hover:border-violet-500/50 hover:bg-white/[0.07] transition-all duration-300 cursor-pointer block"
        >
          <!-- top glow on hover -->
          <div
            class="absolute inset-x-0 top-0 h-px bg-linear-to-r from-transparent via-violet-400/50 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-t-2xl"
          ></div>

          <div class="text-3xl mb-5">{{ project.icon }}</div>

          <h3 class="text-lg font-semibold text-white mb-2">
            {{ project.title }}
          </h3>
          <p class="text-sm text-white/50 leading-relaxed mb-5">
            {{ project.description }}
          </p>

          <div class="flex flex-wrap gap-2 mb-6">
            <span
              v-for="tag in project.tags"
              :key="tag"
              class="text-xs px-3 py-1 rounded-full bg-white/5 border border-white/10 text-white/60"
              >{{ tag }}</span
            >
          </div>

          <div
            class="flex items-center gap-1.5 text-sm text-white/40 group-hover:text-violet-400 transition-colors duration-200"
          >
            <span v-if="project.demo">Live Demo</span>
            <span v-else>GitHub</span>
            <span class="text-xs">↗</span>
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
      "以純 JavaScript 打造的經典貪食蛇遊戲，包含碰撞偵測、分數計算與鍵盤操控邏輯。",
    tags: ["JavaScript", "HTML", "CSS"],
    github: "https://github.com/Nick10744107/Nibbles",
    demo: "https://nick10744107.github.io/Nibbles/",
  },
  {
    icon: "♟️",
    title: "圍棋資訊網",
    description:
      "圍棋知識與資訊平台，涵蓋歷史演進、基本術語，並整合韓、日、中、台四大棋院資源連結。",
    tags: ["HTML", "CSS"],
    github: "https://github.com/Nick10744107/new-resume",
    demo: "https://nick10744107.github.io/new-resume/project1/index.html",
  },
  {
    icon: "🗾",
    title: "日本旅遊推薦網站",
    description:
      "日本旅遊規劃平台，介紹北海道、京都、富士山等熱門景點，並提供行程預約與會員功能。",
    tags: ["HTML", "CSS"],
    github: "https://github.com/Nick10744107/new-resume",
    demo: "https://nick10744107.github.io/new-resume/project2/index.html",
  },
  {
    icon: "🗺️",
    title: "Landmarks iOS App",
    description:
      "使用 Swift + SwiftUI 開發的 iOS 景點導覽應用程式，實作地圖整合與收藏功能。",
    tags: ["Swift", "SwiftUI", "iOS"],
    github: "https://github.com/Nick10744107/Landmarks",
  },
];
</script>
