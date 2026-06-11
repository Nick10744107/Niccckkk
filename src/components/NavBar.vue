<template>
  <nav class="fixed top-0 left-0 right-0 z-50 bg-shell border-b-2 border-ink">
    <div class="max-w-5xl mx-auto px-6 h-16 flex items-center justify-between">
      <a href="#hero" class="flex items-center gap-2 font-pixel text-ink text-lg">
        <span class="w-3 h-3 bg-snake inline-block"></span>NICK
      </a>
      <ul class="flex gap-6 sm:gap-10 font-pixel text-xs sm:text-sm text-ink">
        <li v-for="link in links" :key="link.href">
          <a
            :href="link.href"
            class="hover:text-snake transition-colors duration-150"
            >{{ link.label }}</a
          >
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
const links = [
  { href: '#hero', label: 'HOME' },
  { href: '#projects', label: 'WORK' },
  { href: '#contact', label: 'CONTACT' },
]
</script>
