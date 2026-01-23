<template>
  <section id="contact" class="scroll-mt-20 py-12 md:py-16">
    <div class="mx-auto max-w-6xl px-6">
      <div class="grid gap-16 md:items-start">
        <!-- Right: Form -->
        <div class="bg-white p-8 shadow-2xl md:p-12 mx-auto w-full max-w-3xl">
          <div class="text-center mb-10">
            <h2 class="text-2xl md:text-4xl font-bold tracking-tight text-[#0C2340] uppercase">Demande de Renseignement</h2>
            <div class="mt-6 w-12 h-1 bg-[#968243] mx-auto opacity-30"></div>
          </div>

          <form class="space-y-6" @submit.prevent="handleSubmit">
            <!-- Contact Info -->
            <div class="grid gap-4 sm:grid-cols-2">
              <div>
                <label class="mb-1.5 block text-sm font-medium text-slate-700">Prénom</label>
                <input
                  v-model.trim="form.firstName"
                  class="w-full border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                  placeholder="Jean"
                />
              </div>
              <div>
                <label class="mb-1.5 block text-sm font-medium text-slate-700">Nom</label>
                <input
                  v-model.trim="form.lastName"
                  class="w-full border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                  placeholder="Dupont"
                />
              </div>
            </div>

            <div>
              <label class="mb-1.5 block text-sm font-medium text-slate-700">Email</label>
              <input
                v-model.trim="form.email"
                type="email"
                class="w-full border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                placeholder="jean@exemple.com"
              />
            </div>

            <div>
              <label class="mb-1.5 block text-sm font-medium text-slate-700">Téléphone</label>
              <input
                v-model.trim="form.phone"
                type="tel"
                class="w-full border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                placeholder="+33 ..."
              />
            </div>

            <!-- Interest Selection (Condensed) -->
            <div class="pt-2">
              <label class="mb-4 block text-sm font-semibold uppercase tracking-wider text-slate-400">Centres d'intérêt</label>
              <div class="grid gap-4 sm:grid-cols-3">
                <!-- Real Estate -->
                <label 
                  class="flex items-center gap-3 p-4 border-2 transition cursor-pointer"
                  :class="form.realEstate ? 'border-[#968243] bg-[#968243]/5' : 'border-slate-100'"
                >
                  <input v-model="form.realEstate" type="checkbox" class="h-5 w-5 rounded-none accent-[#968243]" />
                  <span class="font-medium text-slate-800">Immobilier</span>
                </label>

                <!-- Yachting -->
                <label 
                  class="flex items-center gap-3 p-4 border-2 transition cursor-pointer"
                  :class="form.yachting ? 'border-[#968243] bg-[#968243]/5' : 'border-slate-100'"
                >
                  <input v-model="form.yachting" type="checkbox" class="h-5 w-5 rounded-none accent-[#968243]" />
                  <span class="font-medium text-slate-800">Yachting</span>
                </label>

                <!-- Aviation -->
                <label 
                  class="flex items-center gap-3 p-4 border-2 transition cursor-pointer"
                  :class="form.aviation ? 'border-[#968243] bg-[#968243]/5' : 'border-slate-100'"
                >
                  <input v-model="form.aviation" type="checkbox" class="h-5 w-5 rounded-none accent-[#968243]" />
                  <span class="font-medium text-slate-800">Aviation</span>
                </label>
              </div>
            </div>

            <!-- Actions -->
            <div class="space-y-3 pt-4">
              <button
                type="submit"
                class="w-full py-3.5 text-sm font-semibold text-white shadow-lg transition hover:opacity-90 disabled:opacity-50"
                :style="{ backgroundColor: colors.gold }"
                :disabled="submitting"
              >
                {{ submitting ? 'Envoi...' : 'Envoyer la demande' }}
              </button>

              <a
                class="block w-full border border-slate-200 bg-white py-3.5 text-center text-sm font-semibold text-slate-700 transition hover:bg-slate-50"
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
  aviation: false,
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

  if (!form.realEstate && !form.yachting && !form.aviation) {
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
