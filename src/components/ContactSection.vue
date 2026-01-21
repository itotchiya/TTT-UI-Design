<template>
  <section id="contact" class="scroll-mt-20 py-16 md:py-24" :style="{ backgroundColor: colors.blue }">
    <div class="mx-auto max-w-6xl px-4">
      <div class="grid gap-10 md:grid-cols-2 md:items-center">
        <!-- Left: Text -->
        <div class="text-white">
          <h2 class="text-3xl font-bold tracking-tight md:text-4xl">Découvrir le Site</h2>
          <p class="mt-4 text-lg text-white/80">
            Obtenez un accès exclusif à notre catalogue premium. Renseignez vos coordonnées et notre équipe de conciergerie vous contactera avec des recommandations personnalisées.
          </p>
        </div>

        <!-- Right: Form -->
        <div class="rounded-3xl bg-white p-6 shadow-2xl md:p-8">
          <form class="space-y-4" @submit.prevent="handleSubmit">
            <div class="grid gap-4 sm:grid-cols-2">
              <div>
                <label class="mb-1.5 block text-sm font-medium text-slate-700">Prénom</label>
                <input
                  v-model.trim="form.firstName"
                  class="w-full rounded-xl border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                  placeholder="Jean"
                  required
                />
              </div>
              <div>
                <label class="mb-1.5 block text-sm font-medium text-slate-700">Nom</label>
                <input
                  v-model.trim="form.lastName"
                  class="w-full rounded-xl border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                  placeholder="Dupont"
                  required
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
                required
              />
            </div>

            <div>
              <label class="mb-1.5 block text-sm font-medium text-slate-700">Téléphone</label>
              <input
                v-model.trim="form.phone"
                type="tel"
                class="w-full rounded-xl border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                placeholder="+33 ..."
                required
              />
            </div>

            <div>
              <label class="mb-1.5 block text-sm font-medium text-slate-700">Intérêt</label>
              <select
                v-model="form.interest"
                class="w-full rounded-xl border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
              >
                <option value="Immobilier">Immobilier</option>
                <option value="Yachting">Yachting</option>
              </select>
            </div>

            <button
              type="submit"
              class="w-full rounded-xl py-3.5 text-sm font-semibold text-white shadow-lg transition hover:opacity-90 disabled:opacity-50"
              :style="{ backgroundColor: colors.gold }"
              :disabled="submitting"
            >
              {{ submitting ? 'Envoi...' : 'Découvrir Maintenant' }}
            </button>

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
            href="https://new.thetenderto.com/"
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

const form = reactive({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  interest: 'Immobilier',
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
        window.location.href = 'https://new.thetenderto.com/'
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
