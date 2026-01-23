
<template>
  <div class="fixed top-6 right-6 z-[100] flex gap-1 bg-[#0C2340]/20 backdrop-blur-md p-1 rounded-full border border-white/10 shadow-xl">
    <button 
      v-for="lang in ['fr', 'en']" 
      :key="lang"
      @click="setLocale(lang)"
      class="px-4 py-1.5 rounded-full text-xs font-bold uppercase tracking-widest transition-all duration-300"
      :class="[
        locale === lang 
          ? 'bg-[#968243] text-white shadow-md' 
          : 'text-white/70 hover:text-white hover:bg-white/10'
      ]"
    >
      {{ lang }}
    </button>
  </div>
</template>

<script setup>
import { useI18n } from 'vue-i18n'

const { locale } = useI18n()

function setLocale(lang) {
  locale.value = lang
  // Optional: save to localStorage
  localStorage.setItem('user-locale', lang)
}
</script>

<style scoped>
button {
  backdrop-filter: blur(8px);
}
</style>
