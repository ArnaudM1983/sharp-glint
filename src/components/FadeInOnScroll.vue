<template>
  <div ref="container">
    <slot />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { gsap } from 'gsap'

const container = ref(null)

let observer = null

onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      gsap.to(container.value, {
        opacity: 1,
        y: 0,
        duration: 2,
        ease: "power3.out"
      })
      observer.disconnect()
    }
  }, { threshold: 0.1 })

  if (container.value) {
    // Initial state before animation
    gsap.set(container.value, { opacity: 0, y: 50 })
    observer.observe(container.value)
  }
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>
