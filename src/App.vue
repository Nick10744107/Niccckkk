<script setup>
import { onMounted, onUnmounted } from 'vue'

let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      for (const entry of entries) {
        if (entry.isIntersecting) {
          entry.target.classList.add('revealed')
          observer.unobserve(entry.target)
        }
      }
    },
    { threshold: 0.15 }
  )
  document.querySelectorAll('[data-reveal]').forEach((el) => observer.observe(el))
})

onUnmounted(() => observer?.disconnect())
</script>

<template>
  <NavBar />
  <main>
    <HeroSection />
    <PixelMarquee
      variant="snake"
      :items="['INSERT COIN', 'HI-SCORE 9999', 'PRESS START', 'STAGE 1: PORTFOLIO', '1UP']"
    />
    <ProjectsSection />
    <PixelMarquee
      variant="apple"
      :items="['CONTINUE?', 'NEW CHALLENGER APPROACHING', 'SAY HELLO', 'BONUS STAGE']"
    />
    <ContactSection />
  </main>
  <FooterBar />
</template>
