<template>
  <Navbar />

  <main class="bg-black mx-auto space-y-20">
    <Hero />
    <ImageTextSection />
    <Projects />
    <CtaSection />
    <Footer />
  </main>
</template>

<script setup>
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import ImageTextSection from './components/ImageTextSection.vue'
import Projects from './components/Projects.vue'
import CtaSection from './components/CtaSection.vue'
import Footer from './components/Footer.vue'
</script>
