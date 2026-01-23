
<template>
  <div class="fixed top-6 right-6 z-[100] flex gap-1 bg-[#0C2340] border border-[#968243]/30 p-1 rounded-full shadow-2xl">
    <button 
      v-for="lang in ['FR', 'EN']" 
      :key="lang"
      @click="setLocale(lang.toLowerCase())"
      class="px-4 py-1.5 rounded-full text-[10px] font-black uppercase tracking-[0.2em] transition-all duration-300"
      :class="[
        locale === lang.toLowerCase() 
          ? 'bg-[#968243] text-white shadow-lg' 
          : 'text-white/50 hover:text-white hover:bg-white/5'
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
