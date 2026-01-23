<template>
  <section class="py-12 md:py-20">
    <div class="mx-auto max-w-6xl px-6">
      <div class="relative pl-8 md:pl-16 mb-20">
        <!-- Animated Side Border -->
        <div class="absolute left-0 top-0 h-full w-[1px] bg-white/10 overflow-hidden">
          <div class="absolute top-0 left-0 w-full bg-white/40 side-line-fill"></div>
        </div>

        <h2 class="text-2xl md:text-4xl font-bold text-white leading-tight tracking-wider uppercase mb-10">
          Vous portez un intérêt
        </h2>

        <div class="space-y-6 text-white/80 font-light leading-relaxed max-w-2xl text-lg">
          <p>Immobilier, Yachting ou Aviation privée ?</p>
          <p>Veuillez renseigner vos informations <br />et sélectionner le secteur qui vous intéresse.</p>
        </div>
      </div>

      <div class="grid gap-8 md:grid-cols-3">
        <div 
          v-for="sector in sectors" 
          :key="sector.name" 
          class="relative group h-64 overflow-hidden shadow-xl cursor-pointer"
          @click="$emit('select-interest', sector.name)"
        >
          <img 
            :src="sector.image" 
            :alt="sector.name" 
            class="sector-image absolute inset-0 h-[120%] w-full object-cover transition-opacity duration-700" 
          />
          <div class="absolute inset-0 bg-black/40 group-hover:bg-black/20 transition-colors" />
          <div class="absolute inset-0 flex items-center justify-center">
            <div class="relative px-8 py-4">
              <!-- Corner Accent: Bottom Left -->
              <div class="absolute -bottom-1 -left-1 h-4 w-4 border-b border-l border-white/80" />
              <!-- Corner Accent: Top Right -->
              <div class="absolute -top-1 -right-1 h-4 w-4 border-t border-r border-white/80" />
              
              <span class="text-lg md:text-xl font-light text-white tracking-[0.2em] uppercase text-center drop-shadow-md">
                {{ sector.name }}
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="mt-16 text-center">
        <p class="text-white/80 font-medium text-lg mb-8 italic">Merci de compléter le formulaire ci-dessous</p>
        <div class="w-16 h-px bg-white/30 mx-auto"></div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'

const emit = defineEmits(['select-interest'])
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

const sectors = [
  { name: 'IMMOBILIER', image: '/assets/Real-estate.jpg' },
  { name: 'YACHTING', image: '/assets/Yachting.jpg' },
  { name: 'AVIATION', image: '/assets/flights-bg.png' },
]

onMounted(() => {
  gsap.utils.toArray('.sector-image').forEach((img) => {
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
