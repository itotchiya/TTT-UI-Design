<template>
  <section id="presentation" class="relative min-h-[90vh] flex flex-col items-center justify-center pt-16 pb-24 overflow-hidden">
    <!-- Background (Subtle) -->
    <div class="absolute inset-0 z-0">
      <div class="absolute inset-0 bg-gradient-to-b from-[#0C2340]/50 to-[#0C2340]" />
    </div>

    <div class="relative z-10 w-full max-w-6xl px-6 text-center">
      <!-- Logo -->
      <div class="mb-16 flex justify-center">
        <img src="/assets/logo vertical.svg" alt="The Tender To" class="h-48 brightness-0 invert" />
      </div>

      <!-- Welcome Box -->
      <div class="relative mx-auto w-full border border-white/10 p-10 md:p-16">
        <!-- Corner Accent: Bottom Left -->
        <div class="absolute -bottom-2 -left-2 h-12 w-12 border-b-2 border-l-2 border-white/40" />
        <!-- Corner Accent: Top Right -->
        <div class="absolute -top-2 -right-2 h-12 w-12 border-t-2 border-r-2 border-white/40" />

        <h1 class="text-3xl md:text-5xl font-light text-white leading-tight mb-12 uppercase tracking-widest">
          Bienvenue à bord,
        </h1>
        
        <div class="space-y-8 text-left mx-auto">
          <p class="text-lg md:text-xl text-white/90 font-light leading-relaxed">
            The Tender To est une plateforme innovante réunissant trois secteurs phares :<br />
            l’Immobilier, le Yachting et l’Aviation privée.
          </p>

          <p class="text-base md:text-lg text-white/80 font-light leading-relaxed">
            Nous avons conçu un écosystème d’apporteurs d’affaires et de partenaires professionnels afin de connecter clients, biens et opportunités d’exception.<br />
            The Tender To privilégie le réseau, la mise en relation qualifiée et une approche discrète, propre aux univers du luxe.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
</script>
