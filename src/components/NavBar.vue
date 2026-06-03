<template>
  <nav class="fixed top-0 left-0 right-0 z-50 bg-black/80 backdrop-blur-md border-b border-white/10">
    <div class="max-w-6xl mx-auto px-8 h-16 flex items-center justify-between">
      <span class="font-bold text-white text-lg tracking-widest uppercase">Nick.</span>
      <ul class="flex gap-10 text-sm text-white/60 tracking-wider uppercase">
        <li v-for="link in links" :key="link.href">
          <a :href="link.href" class="hover:text-white transition-colors duration-300">{{ link.label }}</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
const links = [
  { href: '#hero', label: 'Home' },
  { href: '#projects', label: 'Work' },
  { href: '#contact', label: 'Contact' },
]
</script>
