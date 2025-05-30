<template>
  <header class="fixed top-0 left-0 w-full bg-black text-white z-50 flex items-center justify-between p-4 md:px-8">

    <!-- Gauche : Lien Accueil -->
    <a href="/"
      class="text-white text-lg uppercase font-light tracking-wide font-inter hidden md:block">
      Accueil
    </a>

    <!-- Centre : Logo -->
    <div class="text-white text-2xl font-light tracking-widest uppercase font-inter">
      Glint
    </div>

    <!-- Droite : Menu Burger -->
    <button @click="isMenuOpen = !isMenuOpen"
      class="w-20 h-10 flex items-center justify-center cursor-pointer transition-all duration-300 z-60">
      <template v-if="!isMenuOpen">
        <div class="flex flex-col justify-center items-center space-y-1">
          <span class="w-10 h-[2px] bg-gray-400"></span>
          <span class="w-10 h-[2px] bg-gray-400"></span>
        </div>
      </template>
      <template v-else>
        <span class="text-lg uppercase font-light tracking-widest font-inter">Fermer</span>
      </template>
    </button>

  </header>

  <!-- Menu Mobile fullscreen sous la navbar -->
  <nav v-if="isMenuOpen"
    class="fixed top-0 left-0 w-screen h-screen bg-black text-white md:text-gray-700 flex flex-col justify-center items-center space-y-12 font-inter text-xl md:text-7xl font-normal tracking-widest z-40 pt-16">

    <a href="#accueil" @click.prevent="scrollToSection('#accueil')" class="hover:text-white">
      Accueil
    </a>
    <a href="#about" @click.prevent="scrollToSection('#about')" class="hover:text-white">
      À propos
    </a>
    <a href="#projets" @click.prevent="scrollToSection('#projets')" class="hover:text-white">
      Projets
    </a>
    <a href="#contact" @click.prevent="scrollToSection('#contact')" class="hover:text-white">
      Contact
    </a>

  </nav>
</template>

<script setup>
import { ref } from 'vue'

const isMenuOpen = ref(false)

const scrollToSection = (id) => {
  isMenuOpen.value = false
  const section = document.querySelector(id)
  if (section) section.scrollIntoView({ behavior: 'smooth' })
}
</script>
