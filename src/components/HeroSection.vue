<template>
  <section id="presentation" class="relative overflow-hidden">
    <!-- Background -->
    <div class="absolute inset-0">
      <img
        src="/assets/Real-estate.jpg"
        alt="Arrière-plan"
        class="h-full w-full object-cover opacity-40"
      />
      <div class="absolute inset-0 bg-gradient-to-r from-white via-white/80 to-white/0" />
    </div>

    <div class="relative mx-auto max-w-6xl px-4 py-24 md:py-32 lg:py-40">
      <div class="max-w-3xl">
        <!-- Badge -->
        <div class="inline-flex items-center gap-2 rounded-full border bg-white/80 px-4 py-2 text-sm font-medium text-slate-600 shadow-sm backdrop-blur">
          <span class="h-2 w-2 rounded-full" :style="{ backgroundColor: colors.gold }" />
          Services de Conciergerie de Luxe
        </div>

        <!-- Title -->
        <h1 class="mt-8 text-4xl font-bold leading-tight tracking-tight md:text-5xl lg:text-6xl">
          Votre Portail vers
          <span class="block" :style="{ color: colors.blue }">un Art de Vivre d'Exception</span>
        </h1>

        <!-- Subtitle -->
        <p class="mt-6 text-xl text-slate-600 md:text-2xl">
          Expériences de luxe en Immobilier & Yachting
        </p>

        <!-- Description -->
        <p class="mt-4 max-w-2xl text-base leading-relaxed text-slate-500 md:text-lg">
          Découvrez des propriétés d'exception dans les destinations les plus prisées au monde et explorez des charters de yachts exclusifs en Méditerranée. Notre équipe de conciergerie vous assure une expérience personnalisée et sans faille, de la première demande à la réservation finale.
        </p>

        <!-- Actions -->
        <div class="mt-10 flex flex-wrap gap-4">
          <button
            class="rounded-full px-8 py-4 text-base font-semibold shadow-lg transition hover:scale-105"
            :style="{ backgroundColor: colors.gold, color: 'white' }"
            @click="$emit('scrollTo', 'contact')"
          >
            Découvrir le Site
          </button>
          <button
            class="rounded-full border-2 border-slate-200 bg-white px-8 py-4 text-base font-semibold text-slate-700 shadow-sm transition hover:border-slate-300 hover:bg-slate-50"
            @click="$emit('scrollTo', 'availability')"
          >
            Voir les Destinations
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
defineEmits(['scrollTo'])

const colors = {
  blue: '#0C2340',
  gold: '#968243',
}
</script>
