<template>
  <footer class="border-t-2 border-ink bg-shell text-center">
    <div class="checker-strip border-b-2 border-ink" aria-hidden="true"></div>
    <div class="py-8 px-6">
    <div class="flex items-center justify-center gap-6 mb-3 font-pixel text-sm">
      <a
        href="https://github.com/Nick10744107"
        target="_blank"
        rel="noopener noreferrer"
        class="text-ink/50 hover:text-snake transition-colors duration-150"
      >
        GITHUB
      </a>
      <span class="text-ink/20">▪</span>
      <a
        href="mailto:jerrychang890309@gmail.com"
        class="text-ink/50 hover:text-snake transition-colors duration-150"
      >
        EMAIL
      </a>
    </div>
    <p class="font-pixel text-xs text-ink/30">
      © {{ new Date().getFullYear() }} NICK · GAME OVER? PRESS F5 TO CONTINUE
    </p>
    </div>
  </footer>
</template>
