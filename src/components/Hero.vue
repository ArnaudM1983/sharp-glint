<template>
    <section class="relative h-dvh w-full bg-black overflow-hidden">
        <!-- Grille en 3 colonnes -->
        <div class="absolute inset-0 z-10 grid grid-cols-1 md:grid-cols-3 place-items-center px-4 md:px-16 text-white">
            <!-- Colonne 1 : Texte gauche -->
            <div :class="[
                'font-inter uppercase text-center text-sm md:text-lg leading-tight font-light tracking-wider opacity-0 animate-fade-in-delayed-1',
                !isMobile ? '-translate-y-20' : 'translate-y-10'
            ]">
                Photographe<br />Indépendant
            </div>


            <!-- Colonne 2 : Image centrale -->
            <div>
                <img :src="heroImage" alt="Hero Image"
                    class="w-[250px] md:w-[330px] object-contain opacity-0 animate-fade-in-up" />
            </div>

            <!-- Colonne 3 : Texte droite (desktop only) -->
            <div v-if="!isMobile"
                class="font-inter uppercase text-center text-sm md:text-lg leading-tight font-light tracking-wider -translate-y-20 opacity-0 animate-fade-in-delayed-1">
                Basé à<br />Lyon
            </div>
        </div>

        <!-- Nom centré bas -->
        <div class="absolute bottom-2 left-1/2 transform -translate-x-1/2 z-10 flex flex-col items-center">
            <h1 ref="titleRef" :class="['text-white uppercase custom-title', { 'mobile-multiline': isMobile }]">
                Sharp Glint
            </h1>

            <!-- Texte Basé à Lyon (mobile only, après h1) -->
            <div v-if="isMobile"
                class="font-inter text-white uppercase text-center text-sm leading-tight font-light tracking-wider mt-4">
                Basé à<br />Lyon
            </div>
        </div>
    </section>
</template>


<script setup>
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import heroImage from '@/assets/hero.png'

gsap.registerPlugin(ScrollTrigger)

const titleRef = ref(null)
const isMobile = ref(false)

onMounted(() => {
    isMobile.value = window.innerWidth < 768

    // Animation d'entrée (desktop + mobile)
    gsap.fromTo(
        titleRef.value,
        { opacity: 0, x: 1000 },
        {
            opacity: 1,
            x: 0,
            duration: 1.5,
            ease: 'power3.out',
            delay: 1.5,
            onComplete: () => {
                if (!isMobile.value) {
                    gsap.set(titleRef.value, { x: 0.1 })
                    gsap.to(titleRef.value, {
                        x: '-30vw',
                        ease: 'none',
                        scrollTrigger: {
                            trigger: titleRef.value,
                            start: 'top center',
                            end: '+=500',
                            scrub: true,
                        },
                    })
                }
            },
        }
    )
})
</script>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&display=swap');

.font-inter {
    font-family: 'Inter', sans-serif;
}

.custom-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 25vw;
    font-weight: 300;
    line-height: 1;
    letter-spacing: 0.5vw;
    white-space: nowrap;
    text-align: center;
}

.mobile-multiline {
    white-space: normal !important;
    font-size: 36vw !important;
    line-height: 0.8 !important;
    max-width: 80vw;
}

@keyframes fadeInUp {
    0% {
        opacity: 0;
        transform: translateY(80px);
    }

    100% {
        opacity: 1;
        transform: translateY(0);
    }
}

.animate-fade-in-up {
    animation: fadeInUp 1s ease-out forwards;
}

@keyframes fadeIn {
    0% {
        opacity: 0;
    }

    100% {
        opacity: 1;
    }
}

.animate-fade-in-delayed-1 {
    animation: fadeIn 1s ease-out 1s forwards;
}
</style>