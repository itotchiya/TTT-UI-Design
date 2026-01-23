<template>
  <section class="relative py-12 md:py-20">
    <div class="mx-auto max-w-6xl px-6">
      <div class="relative pl-8 md:pl-16">
        <!-- Animated Side Border -->
        <div class="absolute left-0 top-0 h-full w-[1px] bg-white/10 overflow-hidden">
          <div class="absolute top-0 left-0 w-full bg-white/40 side-line-fill"></div>
        </div>

        <div class="mb-16">
          <h2 class="text-2xl md:text-4xl font-bold text-white leading-tight tracking-wider uppercase">
            La Force <br />
            <span class="text-2xl md:text-3xl font-light opacity-80 uppercase tracking-wider">de The Tender To</span>
          </h2>
        </div>

        <div class="space-y-12">
          <div class="relative">
            <p class="text-white/80 font-light leading-relaxed max-w-2xl text-lg">
              <span class="font-bold text-white">Les GoldTender</span> sont des apporteurs d’affaires qualifiés, évoluant dans des environnements haut de gamme et de services premium. <br />
              Ils mettent en relation clients et opportunités grâce à leur réseau et à leur connaissance des attentes d’une clientèle exigeante.
            </p>
          </div>

          <div class="relative">
            <p class="text-white/80 font-light leading-relaxed max-w-2xl text-lg">
              <span class="font-bold text-white">Les InterTender</span> sont des structures professionnelles reconnues — agences, courtiers, acteurs spécialisés — qui collaborent avec The Tender To au sein de l’écosystème.
            </p>
          </div>

          <p class="text-lg text-white font-light pt-8 border-t border-white/10 max-w-2xl leading-relaxed">
            The Tender To coordonne l’ensemble des mises en relation afin d’assurer un fonctionnement fluide, confidentiel et cohérent.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
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
