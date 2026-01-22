<template>
  <div class="min-h-screen" :style="{ backgroundColor: colors.blue }">
    <!-- Sections -->
    <HeroSection @scroll-to="scrollTo" />
    <ForceSection />
    <RegionsSection />
    <SectorsSection />
    <ContactSection />

    <!-- Footer -->
    <footer class="border-t border-white/10 py-12" :style="{ backgroundColor: colors.blue }">
      <div class="mx-auto max-w-6xl px-4">
        <div class="flex flex-col items-center justify-between gap-6 text-sm text-white/50 sm:flex-row">
          <div class="flex items-center gap-4">
            <img src="/assets/logo.png" alt="The Tender To" class="h-8 brightness-0 invert opacity-80" />
            <span>© {{ new Date().getFullYear() }} The Tender To</span>
          </div>
          <div class="flex gap-8">
            <button class="hover:text-white transition-colors" @click="scrollTo('presentation')">Présentation</button>
            <button class="hover:text-white transition-colors" @click="scrollTo('contact')">Contact</button>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import Lenis from 'lenis'

import HeroSection from './components/HeroSection.vue'
import ForceSection from './components/ForceSection.vue'
import RegionsSection from './components/RegionsSection.vue'
import SectorsSection from './components/SectorsSection.vue'
import ContactSection from './components/ContactSection.vue'

gsap.registerPlugin(ScrollTrigger)

let lenis = null

const colors = {
  blue: '#0C2340',
  gold: '#968243',
}

function scrollTo(id) {
  if (lenis) {
    lenis.scrollTo(`#${id}`)
  } else {
    const el = document.getElementById(id)
    if (el) el.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  // Initialize Lenis
  lenis = new Lenis({
    duration: 1.2,
    easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
    smoothWheel: true,
  })

  // Sync ScrollTrigger with Lenis
  lenis.on('scroll', ScrollTrigger.update)

  gsap.ticker.add((time) => {
    lenis.raf(time * 1000)
  })

  gsap.ticker.lagSmoothing(0)

  // Section animations
  gsap.utils.toArray('section').forEach((section) => {
    gsap.from(section, {
      opacity: 0,
      y: 30,
      duration: 1,
      ease: 'power2.out',
      scrollTrigger: {
        trigger: section,
        start: 'top 85%',
      },
    })
  })
})

onUnmounted(() => {
  if (lenis) {
    lenis.destroy()
    lenis = null
  }
  ScrollTrigger.getAll().forEach(t => t.kill())
})
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;700&display=swap');

body {
  font-family: 'Outfit', sans-serif;
  margin: 0;
  -webkit-font-smoothing: antialiased;
}
</style>
