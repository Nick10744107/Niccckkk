<template>
  <section
    id="hero"
    class="min-h-screen bg-shell dot-grid flex items-center pt-24 pb-16 px-6"
  >
    <div
      class="max-w-5xl mx-auto w-full grid lg:grid-cols-2 gap-12 items-center"
    >
      <!-- left: intro -->
      <div>
        <div
          class="inline-flex items-center gap-2 font-pixel text-xs sm:text-sm text-ink border-2 border-ink bg-white px-3 py-1.5 mb-8"
        >
          <span class="w-2 h-2 bg-snake animate-blink-px"></span>
          PLAYER 1 — AVAILABLE FOR WORK
        </div>

        <h1 class="font-pixel text-5xl sm:text-6xl text-ink leading-tight mb-4">
          嗨,我是
          <span class="text-snake [text-shadow:4px_4px_0_#0b2440]">Nick</span>
        </h1>

        <p
          class="font-pixel text-sm sm:text-base text-ink/60 tracking-wide mb-6"
        >
          FULL-STACK DEVELOPER · ML ENGINEER
        </p>

        <p class="text-lg text-ink/70 leading-relaxed mb-10 max-w-md">
          中原大學資管所碩士,喜歡網頁開發與機器學習,喜歡用程式碼解決真實問題
        </p>

        <div class="flex gap-4 flex-wrap">
          <a
            href="#projects"
            class="pixel-box font-pixel bg-snake text-white px-7 py-3 text-sm sm:text-base hover:-translate-x-0.5 hover:-translate-y-0.5 hover:shadow-[6px_6px_0_0_#0b2440] transition-all duration-150"
          >
            查看作品 ▸
          </a>
          <a
            href="#contact"
            class="pixel-box font-pixel bg-white text-ink px-7 py-3 text-sm sm:text-base hover:-translate-x-0.5 hover:-translate-y-0.5 hover:shadow-[6px_6px_0_0_#0b2440] transition-all duration-150"
          >
            聯絡我
          </a>
        </div>
      </div>

      <!-- right: the playable thing -->
      <SnakeScreen />
    </div>
  </section>
</template>
