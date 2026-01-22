<template>
  <section class="py-20 md:py-32 bg-[#0C2340]">
    <div class="mx-auto max-w-6xl px-6">
      <div class="mb-20 border-l border-white/10 pl-8 md:pl-16">
        <h2 class="text-4xl md:text-5xl font-bold text-white mb-4 uppercase tracking-wider">Où nous opérons</h2>
        <p class="mt-6 text-lg text-white/70 font-light max-w-2xl">
          Grâce à son réseau, The Tender To est implanté dans des univers <span class="font-bold text-white">iconiques</span>, luxueux et hautement spécialisés.
        </p>
      </div>

      <div class="grid gap-8 md:grid-cols-2">
        <div v-for="city in cities" :key="city.name" class="relative group h-64 md:h-80 overflow-hidden">
          <img :src="city.image" :alt="city.name" class="h-full w-full object-cover transition-transform duration-1000 group-hover:scale-105" />
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
const cities = [
  { name: 'MEGEVE', image: '/assets/MEGEVE.jpg' },
  { name: 'MARRAKECH', image: '/assets/Marrakesh.jpg' },
  { name: 'ST TROPEZ', image: '/assets/ST-TROPEZ.webp' },
  { name: 'PARIS', image: '/assets/paris.jpg' },
]
</script>
