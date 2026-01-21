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

    <div class="relative mx-auto max-w-6xl px-4 py-20 md:py-28 lg:py-36">
      <div class="max-w-3xl">
        <!-- Logo -->
        <img src="/assets/logo.png" alt="The Tender To" class="h-14 md:h-16" />

        <!-- Title -->
        <h1 class="mt-8 text-4xl font-bold leading-tight tracking-tight md:text-5xl lg:text-6xl">
          Votre Portail vers
          <span class="block" :style="{ color: colors.blue }">un Art de Vivre d'Exception</span>
        </h1>

        <!-- Description -->
        <p class="mt-6 max-w-2xl text-base leading-relaxed text-slate-600 md:text-lg">
          Découvrez des propriétés d'exception dans les destinations les plus prisées au monde et explorez des charters de yachts exclusifs en Méditerranée. Notre équipe de conciergerie vous assure une expérience personnalisée et sans faille.
        </p>

        <!-- Single Action -->
        <div class="mt-10">
          <button
            class="rounded-full px-8 py-4 text-base font-semibold shadow-lg transition hover:scale-105"
            :style="{ backgroundColor: colors.gold, color: 'white' }"
            @click="$emit('scrollTo', 'contact')"
          >
            Découvrir le Site
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
