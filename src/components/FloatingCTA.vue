
<template>
  <Transition name="slide-up">
    <div 
      v-if="isVisible" 
      class="fixed bottom-0 z-50 w-full bg-[#968243] shadow-[0_-10px_40px_rgba(0,0,0,0.3)]"
    >
      <div 
        @click="scrollToContact"
        class="group relative cursor-pointer overflow-hidden py-4 md:py-5 text-center"
      >
        <span class="text-sm md:text-lg font-bold uppercase tracking-widest text-white drop-shadow-sm transition-transform group-hover:scale-105">
          Demande de Renseignement
        </span>
      </div>
    </div>
  </Transition>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isVisible = ref(true)

function scrollToContact() {
  const el = document.getElementById('contact')
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    // If contact section is intersecting (visible), hide the button
    // If NOT intersecting (not visible), show the button
    isVisible.value = !entries[0].isIntersecting
  }, {
    root: null,
    threshold: 0.1 // Activate when 10% of contact section is visible
  })

  const contactSection = document.getElementById('contact')
  if (contactSection) {
    observer.observe(contactSection)
  }

  onUnmounted(() => {
    observer.disconnect()
  })
})
</script>

<style scoped>
.slide-up-enter-active,
.slide-up-leave-active {
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.4s ease;
}

.slide-up-enter-from,
.slide-up-leave-to {
  transform: translateY(100%);
  opacity: 0;
}
</style>
