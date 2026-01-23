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
            {{ $t('force.title') }} <br />
            <span class="text-2xl md:text-3xl font-light opacity-80 uppercase tracking-wider">{{ $t('force.subtitle') }}</span>
          </h2>
        </div>

        <div class="space-y-12">
          <div class="relative">
            <p class="text-white/80 font-light leading-relaxed max-w-2xl text-lg">
              <span class="font-bold text-white">{{ $t('force.goldTender') }}</span> {{ $t('force.goldTenderDesc') }} <br />
              {{ $t('force.goldTenderDesc2') }}
            </p>
          </div>

          <div class="relative">
            <p class="text-white/80 font-light leading-relaxed max-w-2xl text-lg">
              <span class="font-bold text-white">{{ $t('force.interTender') }}</span> {{ $t('force.interTenderDesc') }}
            </p>
          </div>

          <p class="text-lg text-white font-light pt-8 border-t border-white/10 max-w-2xl leading-relaxed">
            {{ $t('force.coordination') }}
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
