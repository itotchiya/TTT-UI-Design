<template>
  <section id="contact" class="scroll-mt-20 py-16 md:py-24" :style="{ backgroundColor: colors.blue }">
    <div class="mx-auto max-w-6xl px-4">
      <div class="grid gap-10 md:grid-cols-2 md:items-start">
        <!-- Left: Text -->
        <div class="text-white md:sticky md:top-24">
          <h2 class="text-3xl font-bold tracking-tight md:text-4xl">Découvrir le Site</h2>
          <p class="mt-4 text-lg text-white/80">
            Remplissez le formulaire et sélectionnez vos centres d'intérêt pour accéder à notre catalogue premium. Notre équipe de conciergerie vous contactera avec des recommandations personnalisées.
          </p>
        </div>

        <!-- Right: Form -->
        <div class="rounded-3xl bg-white p-6 shadow-2xl md:p-8">
          <form class="space-y-4" @submit.prevent="handleSubmit">
            <!-- Contact Info -->
            <div class="grid gap-4 sm:grid-cols-2">
              <div>
                <label class="mb-1.5 block text-sm font-medium text-slate-700">Prénom</label>
                <input
                  v-model.trim="form.firstName"
                  class="w-full rounded-xl border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                  placeholder="Jean"
                />
              </div>
              <div>
                <label class="mb-1.5 block text-sm font-medium text-slate-700">Nom</label>
                <input
                  v-model.trim="form.lastName"
                  class="w-full rounded-xl border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                  placeholder="Dupont"
                />
              </div>
            </div>

            <div>
              <label class="mb-1.5 block text-sm font-medium text-slate-700">Email</label>
              <input
                v-model.trim="form.email"
                type="email"
                class="w-full rounded-xl border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                placeholder="jean@exemple.com"
              />
            </div>

            <div>
              <label class="mb-1.5 block text-sm font-medium text-slate-700">Téléphone</label>
              <input
                v-model.trim="form.phone"
                type="tel"
                class="w-full rounded-xl border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                placeholder="+33 ..."
              />
            </div>

            <!-- Interest Selection (Below inputs) -->
            <div class="pt-2">
              <label class="mb-3 block text-sm font-medium text-slate-700">Vos centres d'intérêt</label>
              <div class="space-y-3">
                <!-- Real Estate -->
                <div
                  class="rounded-xl border-2 transition"
                  :class="form.realEstate ? 'border-[#968243]' : 'border-slate-200'"
                >
                  <label
                    class="flex cursor-pointer items-center gap-3 p-3"
                    :class="form.realEstate ? 'bg-[#968243]/5' : ''"
                  >
                    <input
                      v-model="form.realEstate"
                      type="checkbox"
                      class="h-5 w-5 rounded accent-[#968243]"
                    />
                    <div class="flex-1">
                      <div class="font-medium text-slate-800">Immobilier</div>
                      <div class="text-xs text-slate-500">Propriétés de luxe</div>
                    </div>
                    <svg
                      class="h-5 w-5 text-slate-400 transition-transform"
                      :class="form.realEstate ? 'rotate-180' : ''"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                    </svg>
                  </label>

                  <!-- Real Estate Cities -->
                  <div v-if="form.realEstate" class="border-t border-slate-100 p-3">
                    <div class="mb-2 text-xs font-medium text-slate-500">Sélectionnez vos destinations</div>
                    <div class="grid gap-2 sm:grid-cols-2">
                      <label
                        v-for="city in realEstateCities"
                        :key="city.name"
                        class="flex cursor-pointer items-center gap-2 rounded-lg border px-3 py-2 transition"
                        :class="form.selectedRealEstateCities.includes(city.name) ? 'border-[#968243] bg-[#968243]/5' : 'border-slate-100 hover:border-slate-200'"
                      >
                        <input
                          v-model="form.selectedRealEstateCities"
                          type="checkbox"
                          :value="city.name"
                          class="h-4 w-4 rounded accent-[#968243]"
                        />
                        <img :src="city.flag" :alt="city.country" class="h-4 w-6 rounded object-cover" />
                        <span class="text-sm text-slate-700">{{ city.name }}</span>
                      </label>
                    </div>
                  </div>
                </div>

                <!-- Yachting -->
                <div
                  class="rounded-xl border-2 transition"
                  :class="form.yachting ? 'border-[#968243]' : 'border-slate-200'"
                >
                  <label
                    class="flex cursor-pointer items-center gap-3 p-3"
                    :class="form.yachting ? 'bg-[#968243]/5' : ''"
                  >
                    <input
                      v-model="form.yachting"
                      type="checkbox"
                      class="h-5 w-5 rounded accent-[#968243]"
                    />
                    <div class="flex-1">
                      <div class="font-medium text-slate-800">Yachting</div>
                      <div class="text-xs text-slate-500">Charters & croisières</div>
                    </div>
                    <svg
                      class="h-5 w-5 text-slate-400 transition-transform"
                      :class="form.yachting ? 'rotate-180' : ''"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                    </svg>
                  </label>

                  <!-- Yachting Cities -->
                  <div v-if="form.yachting" class="border-t border-slate-100 p-3">
                    <div class="mb-2 text-xs font-medium text-slate-500">Sélectionnez vos destinations</div>
                    <div class="grid gap-2 sm:grid-cols-2">
                      <label
                        v-for="city in yachtingCities"
                        :key="city.name"
                        class="flex cursor-pointer items-center gap-2 rounded-lg border px-3 py-2 transition"
                        :class="form.selectedYachtingCities.includes(city.name) ? 'border-[#968243] bg-[#968243]/5' : 'border-slate-100 hover:border-slate-200'"
                      >
                        <input
                          v-model="form.selectedYachtingCities"
                          type="checkbox"
                          :value="city.name"
                          class="h-4 w-4 rounded accent-[#968243]"
                        />
                        <img :src="city.flag" :alt="city.country" class="h-4 w-6 rounded object-cover" />
                        <span class="text-sm text-slate-700">{{ city.name }}</span>
                      </label>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Actions -->
            <div class="space-y-3 pt-4">
              <button
                type="submit"
                class="w-full rounded-xl py-3.5 text-sm font-semibold text-white shadow-lg transition hover:opacity-90 disabled:opacity-50"
                :style="{ backgroundColor: colors.gold }"
                :disabled="submitting"
              >
                {{ submitting ? 'Envoi...' : 'Découvrir Maintenant' }}
              </button>

              <a
                class="block w-full rounded-xl border border-slate-200 bg-white py-3.5 text-center text-sm font-semibold text-slate-700 transition hover:bg-slate-50"
                href="https://thetenderto.com/"
                target="_blank"
              >
                Découvrir sans remplir le formulaire
              </a>
            </div>

            <p v-if="error" class="rounded-lg bg-red-50 p-3 text-sm text-red-600">
              {{ error }}
            </p>
          </form>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <div v-if="modalOpen" class="fixed inset-0 z-[60] flex items-center justify-center bg-black/50 p-4" @click.self="closeModal">
      <div class="w-full max-w-md rounded-3xl bg-white p-6 shadow-2xl md:p-8">
        <div class="text-center">
          <div class="mx-auto flex h-14 w-14 items-center justify-center rounded-full" :style="{ backgroundColor: colors.gold }">
            <svg class="h-7 w-7 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <h3 class="mt-4 text-xl font-bold text-slate-900">Vérifiez vos emails</h3>
          <p class="mt-2 text-slate-600">
            Nous avons envoyé un lien de vérification à <strong>{{ form.email }}</strong>
          </p>
        </div>

        <div class="mt-6 rounded-2xl bg-slate-50 p-4">
          <div class="flex items-center justify-between">
            <span class="text-sm font-medium text-slate-700">Redirection dans</span>
            <span class="rounded-full px-3 py-1 text-sm font-bold text-white" :style="{ backgroundColor: colors.blue }">
              {{ countdown }}s
            </span>
          </div>
          <div class="mt-3 h-2 overflow-hidden rounded-full bg-slate-200">
            <div
              class="h-full rounded-full transition-all duration-1000"
              :style="{
                width: `${progressPercent}%`,
                backgroundColor: colors.gold
              }"
            />
          </div>
        </div>

        <div class="mt-6 flex gap-3">
          <a
            class="flex-1 rounded-xl py-3 text-center text-sm font-semibold text-white shadow transition hover:opacity-90"
            :style="{ backgroundColor: colors.blue }"
            href="https://thetenderto.com/"
            target="_blank"
          >
            Ouvrir maintenant
          </a>
          <button
            class="flex-1 rounded-xl border border-slate-200 bg-white py-3 text-sm font-semibold text-slate-700 transition hover:bg-slate-50"
            @click="closeModal"
          >
            Fermer
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive, ref, computed, onUnmounted } from 'vue'

const colors = {
  blue: '#0C2340',
  gold: '#968243',
}

const realEstateCities = [
  { name: 'Paris', country: 'France', flag: '/assets/Flag-France.webp' },
  { name: 'Megève', country: 'France', flag: '/assets/Flag-France.webp' },
  { name: 'Deauville', country: 'France', flag: '/assets/Flag-France.webp' },
  { name: 'Saint-Tropez', country: 'France', flag: '/assets/Flag-France.webp' },
  { name: 'Marrakech', country: 'Maroc', flag: '/assets/Flag_of_Morocco.svg.png' },
]

const yachtingCities = [
  { name: 'Saint-Tropez', country: 'France', flag: '/assets/Flag-France.webp' },
  { name: 'Cannes', country: 'France', flag: '/assets/Flag-France.webp' },
  { name: 'Nice', country: 'France', flag: '/assets/Flag-France.webp' },
  { name: 'Monaco', country: 'Monaco', flag: '/assets/Flag_of_Monaco.svg.webp' },
  { name: 'Ibiza', country: 'Espagne', flag: '/assets/Bandera_de_España.svg' },
]

const form = reactive({
  realEstate: false,
  yachting: false,
  selectedRealEstateCities: [],
  selectedYachtingCities: [],
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
})

const submitting = ref(false)
const error = ref('')
const modalOpen = ref(false)
const countdown = ref(7)
const countdownStart = 7
let timer = null

const progressPercent = computed(() => {
  const done = countdownStart - countdown.value
  return Math.max(0, Math.min(100, (done / countdownStart) * 100))
})

function closeModal() {
  modalOpen.value = false
  if (timer) {
    clearInterval(timer)
    timer = null
  }
  countdown.value = countdownStart
}

async function handleSubmit() {
  error.value = ''

  if (!form.realEstate && !form.yachting) {
    error.value = 'Veuillez sélectionner au moins un centre d\'intérêt.'
    return
  }

  if (!form.firstName || !form.lastName || !form.email || !form.phone) {
    error.value = 'Veuillez remplir tous les champs.'
    return
  }

  submitting.value = true
  try {
    await new Promise(r => setTimeout(r, 700))
    modalOpen.value = true
    countdown.value = countdownStart

    if (timer) clearInterval(timer)
    timer = setInterval(() => {
      countdown.value -= 1
      if (countdown.value <= 0) {
        clearInterval(timer)
        timer = null
        window.location.href = 'https://thetenderto.com/'
      }
    }, 1000)
  } catch {
    error.value = 'Une erreur est survenue. Veuillez réessayer.'
  } finally {
    submitting.value = false
  }
}

onUnmounted(() => {
  if (timer) clearInterval(timer)
})
</script>
