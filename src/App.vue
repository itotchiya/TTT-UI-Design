<template>
  <div class="min-h-screen bg-white text-slate-900">
    <!-- Sections -->
    <HeroSection @scroll-to="scrollTo" />
    <ContactSection />

    <!-- Footer -->
    <footer class="border-t bg-white py-8">
      <div class="mx-auto max-w-6xl px-4">
        <div class="flex flex-col items-center justify-between gap-4 text-sm text-slate-500 sm:flex-row">
          <div class="flex items-center gap-3">
            <img src="/assets/logo.png" alt="The Tender To" class="h-6 opacity-60" />
            <span>© {{ new Date().getFullYear() }} The Tender To</span>
          </div>
          <button class="hover:text-slate-700" @click="scrollTo('presentation')">Retour en haut</button>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

import HeroSection from './components/HeroSection.vue'
import ContactSection from './components/ContactSection.vue'

gsap.registerPlugin(ScrollTrigger)

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}

onMounted(() => {
  gsap.utils.toArray('section').forEach((section) => {
    gsap.from(section, {
      opacity: 0,
      y: 30,
      duration: 0.8,
      ease: 'power2.out',
      scrollTrigger: {
        trigger: section,
        start: 'top 85%',
      },
    })
  })
})

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(t => t.kill())
})
</script>
