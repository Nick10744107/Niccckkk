<template>
  <section id="hero" class="relative min-h-screen flex items-center justify-center bg-black overflow-hidden">
    <!-- background grid -->
    <div class="absolute inset-0 bg-[linear-gradient(rgba(255,255,255,0.03)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.03)_1px,transparent_1px)] bg-[size:72px_72px]"></div>
    <!-- glow -->
    <div class="absolute top-1/3 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-violet-600/20 rounded-full blur-[120px] pointer-events-none"></div>

    <div class="relative z-10 text-center max-w-3xl px-6">
      <!-- badge -->
      <div class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full border border-violet-500/40 bg-violet-500/10 text-violet-300 text-xs tracking-widest uppercase mb-8">
        <span class="w-1.5 h-1.5 rounded-full bg-violet-400 animate-pulse"></span>
        Available for work
      </div>

      <h1 class="text-6xl md:text-7xl font-bold text-white leading-tight mb-6 tracking-tight">
        Hi, I'm <span class="bg-gradient-to-r from-violet-400 to-pink-400 bg-clip-text text-transparent">Nick</span>
      </h1>

      <p class="text-xl text-white/50 mb-10 leading-relaxed max-w-xl mx-auto">
        中原大學資管所碩士，熱愛網頁開發與機器學習，喜歡用程式碼解決真實問題。
      </p>

      <div class="flex gap-4 justify-center flex-wrap">
        <a href="#projects" class="px-8 py-3.5 bg-white text-black rounded-full font-semibold hover:bg-white/90 transition-all duration-300 hover:scale-105">
          查看作品
        </a>
        <a href="#contact" class="px-8 py-3.5 border border-white/20 text-white rounded-full font-semibold hover:border-white/50 hover:bg-white/5 transition-all duration-300">
          聯絡我
        </a>
      </div>

      <!-- scroll hint -->
      <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 text-white/30 text-xs tracking-widest uppercase">
        <span>Scroll</span>
        <div class="w-px h-10 bg-gradient-to-b from-white/30 to-transparent"></div>
      </div>
    </div>
  </section>
</template>
