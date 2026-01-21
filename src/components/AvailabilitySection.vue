<template>
  <section id="availability" class="scroll-mt-20 bg-white py-16 md:py-24">
    <div class="mx-auto max-w-6xl px-4">
      <div class="text-center">
        <h2 class="text-3xl font-bold tracking-tight md:text-4xl">Vous êtes intéressé par ?</h2>
      </div>

      <!-- Feature Cards as Tabs -->
      <div class="mt-10 flex justify-center gap-6">
        <button
          v-for="feature in features"
          :key="feature.id"
          class="group relative w-64 overflow-hidden rounded-2xl shadow-lg transition-all duration-300"
          :class="activeTab === feature.id ? 'ring-4 ring-offset-2 scale-105' : 'opacity-80 hover:opacity-100'"
          :style="activeTab === feature.id ? { ringColor: colors.gold } : {}"
          @click="activeTab = feature.id"
        >
          <img :src="feature.image" :alt="feature.title" class="h-40 w-full object-cover" />
          <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/30 to-transparent" />
          <div class="absolute bottom-4 left-4 right-4">
            <div class="text-lg font-semibold text-white">{{ feature.title }}</div>
          </div>
          <div
            v-if="activeTab === feature.id"
            class="absolute top-3 right-3 rounded-full px-2 py-1 text-xs font-bold"
            :style="{ backgroundColor: colors.gold, color: 'white' }"
          >
            Sélectionné
          </div>
        </button>
      </div>

      <!-- City List -->
      <div class="mx-auto mt-12 max-w-2xl">
        <div class="rounded-3xl border bg-white p-6 shadow-sm">
          <div class="mb-4 flex items-center justify-between">
            <h3 class="text-lg font-semibold text-slate-800">
              {{ activeTab === 'real-estate' ? 'Propriétés' : 'Destinations Charter' }}
            </h3>
            <span
              class="rounded-full px-3 py-1 text-xs font-semibold text-white"
              :style="{ backgroundColor: colors.blue }"
            >
              {{ currentCities.length }} destinations
            </span>
          </div>

          <transition :name="slideDirection" mode="out-in">
            <ul :key="activeTab" class="divide-y divide-slate-100">
              <li
                v-for="city in currentCities"
                :key="city.name"
                class="flex items-center justify-between py-4 first:pt-0 last:pb-0"
              >
                <div class="flex items-center gap-4">
                  <img :src="city.flag" :alt="city.country" class="h-6 w-8 rounded object-cover shadow-sm" />
                  <div>
                    <div class="font-semibold text-slate-900">{{ city.name }}</div>
                    <div class="text-sm text-slate-500">{{ city.country }}</div>
                  </div>
                </div>
                <span
                  class="rounded-full px-3 py-1 text-xs font-medium"
                  :class="city.available ? '' : 'bg-slate-100 text-slate-500'"
                  :style="city.available ? { backgroundColor: colors.gold + '25', color: colors.gold } : {}"
                >
                  {{ city.available ? 'Disponible' : 'Bientôt' }}
                </span>
              </li>
            </ul>
          </transition>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const colors = {
  blue: '#0C2340',
  gold: '#968243',
}

const features = [
  {
    id: 'real-estate',
    title: 'Immobilier',
    image: '/assets/Real-estate.jpg',
  },
  {
    id: 'yachting',
    title: 'Yachting',
    image: '/assets/Yachting.jpg',
  },
]

const activeTab = ref('real-estate')
const slideDirection = ref('slide-left')

watch(activeTab, (newVal, oldVal) => {
  const oldIndex = features.findIndex(f => f.id === oldVal)
  const newIndex = features.findIndex(f => f.id === newVal)
  slideDirection.value = newIndex > oldIndex ? 'slide-left' : 'slide-right'
})

const realEstateCities = [
  { name: 'Paris', country: 'France', flag: '/assets/Flag-France.webp', available: true },
  { name: 'Megève', country: 'France', flag: '/assets/Flag-France.webp', available: true },
  { name: 'Deauville', country: 'France', flag: '/assets/Flag-France.webp', available: false },
  { name: 'Saint-Tropez', country: 'France', flag: '/assets/Flag-France.webp', available: true },
  { name: 'Marrakech', country: 'Maroc', flag: '/assets/Flag_of_Morocco.svg.png', available: false },
]

const yachtingCities = [
  { name: 'Saint-Tropez', country: 'France', flag: '/assets/Flag-France.webp', available: true },
  { name: 'Cannes', country: 'France', flag: '/assets/Flag-France.webp', available: true },
  { name: 'Nice', country: 'France', flag: '/assets/Flag-France.webp', available: false },
  { name: 'Monaco', country: 'Monaco', flag: '/assets/Flag_of_Monaco.svg.webp', available: true },
  { name: 'Ibiza', country: 'Espagne', flag: '/assets/Bandera_de_España.svg', available: false },
]

const currentCities = computed(() =>
  activeTab.value === 'real-estate' ? realEstateCities : yachtingCities
)
</script>

<style scoped>
.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition: all 0.3s ease-out;
}

.slide-left-enter-from {
  opacity: 0;
  transform: translateX(30px);
}
.slide-left-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

.slide-right-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}
.slide-right-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
