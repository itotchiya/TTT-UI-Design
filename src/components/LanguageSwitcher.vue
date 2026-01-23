
<template>
  <div class="fixed top-6 right-6 z-[100] flex gap-2">
    <button 
      v-for="lang in ['fr', 'en']" 
      :key="lang"
      @click="setLocale(lang)"
      class="px-3 py-1.5 rounded-full text-xs font-bold uppercase tracking-widest transition-all duration-300 border shadow-lg"
      :class="[
        locale === lang 
          ? 'bg-white text-[#0C2340] border-white' 
          : 'bg-transparent text-white border-white/30 hover:bg-white/10 hover:border-white'
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
