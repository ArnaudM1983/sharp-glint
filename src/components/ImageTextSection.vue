<script setup>
import plage from '@/assets/plage.png'
import deco from '@/assets/deco.png'
import plage2 from '@/assets/plage2.png'
import FadeInOnScroll from '@/components/FadeInOnScroll.vue'

</script>

<template>
  <!-- Image à gauche et Texte à droite sur desktop -->
  <section>
    <div class="mx-auto max-w-[1250px] px-4 py-8 sm:px-6 lg:px-0">
      <div class="grid grid-cols-1 gap-4 md:grid-cols-2 md:items-start md:gap-24">
        <FadeInOnScroll>
          <div class="md:order-1">
            <p class="text-zinc-300 text-left text-xl md:text-2xl uppercase font-light">à propos de moi</p>
          </div>
        </FadeInOnScroll>
        <div class="md:order-2">
          <div class="max-w-lg md:max-w-none text-left">
            <p class="text-zinc-300 text-xl md:text-2xl font-extralight">
              Sharp Glint capture l’essence même du calme et de la simplicité, à travers des images épurées où chaque
              détail compte. Son univers photographique se distingue par une maîtrise subtile de la lumière naturelle,
              qui caresse délicatement les formes et les textures, créant des ambiances empreintes de douceur et de
              sérénité.
              <br><br>
              Dans ses compositions, Sharp Glint privilégie les espaces vides, non comme un vide à combler, mais comme
              un souffle, une respiration qui invite le regard à se poser, à réfléchir. Les formes géométriques, les
              lignes pures et les textures fines s’entrelacent harmonieusement, donnant naissance à une esthétique
              minimaliste et raffinée.
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>

</template>
