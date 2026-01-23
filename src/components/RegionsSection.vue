<template>
  <section class="py-12 md:py-20 bg-[#0C2340]">
    <div class="mx-auto max-w-6xl px-6">
      <div class="mb-12 relative pl-8 md:pl-16">
        <!-- Animated Side Border -->
        <div class="absolute left-0 top-0 h-full w-[1px] bg-white/10 overflow-hidden">
          <div class="absolute top-0 left-0 w-full bg-white/40 side-line-fill"></div>
        </div>
        
        <h2 class="text-2xl md:text-4xl font-bold text-white leading-tight tracking-wider uppercase mb-10">Où nous opérons</h2>
        <p class="mt-6 text-lg text-white/70 font-light max-w-2xl">
          Grâce à son réseau, The Tender To est implanté dans des univers <span class="font-bold text-white">iconiques</span>, luxueux et hautement spécialisés.
        </p>
      </div>

      <div class="grid gap-8 md:grid-cols-2">
        <div v-for="city in cities" :key="city.name" class="relative group h-64 md:h-80 overflow-hidden">
          <img 
            :src="city.image" 
            :alt="city.name" 
            class="city-image absolute inset-0 h-[120%] w-full object-cover transition-opacity duration-700" 
          />
          <div class="absolute inset-0 bg-black/20 group-hover:bg-black/10 transition-colors" />
          <div class="absolute inset-0 flex items-center justify-center">
            <div class="relative px-12 py-6">
              <!-- Corner Accent: Bottom Left -->
              <div class="absolute -bottom-1 -left-1 h-6 w-6 border-b-2 border-l-2 border-white/60" />
              <!-- Corner Accent: Top Right -->
              <div class="absolute -top-1 -right-1 h-6 w-6 border-t-2 border-r-2 border-white/60" />
              
              <span class="text-xl md:text-3xl font-light text-white tracking-[0.3em] uppercase">
                {{ city.name }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

const cities = [
  { name: 'MEGEVE', image: '/assets/MEGEVE.jpg' },
  { name: 'MARRAKECH', image: '/assets/Marrakesh.jpg' },
  { name: 'ST TROPEZ', image: '/assets/ST-TROPEZ.webp' },
  { name: 'PARIS', image: '/assets/paris.jpg' },
]

onMounted(() => {
  gsap.utils.toArray('.city-image').forEach((img) => {
    gsap.to(img, {
      y: '-20%',
      ease: 'none',
      scrollTrigger: {
        trigger: img.parentElement,
        start: 'top bottom',
        end: 'bottom top',
        scrub: true,
      },
    })
  })
})
</script>

<style scoped>
.side-line-fill {
  height: 30%;
  animation: side-fill 4s cubic-bezier(0.65, 0, 0.35, 1) infinite;
}

@keyframes side-fill {
  0% { transform: translateY(-100%); }
  50% { transform: translateY(400%); }
  100% { transform: translateY(400%); }
}
</style>
