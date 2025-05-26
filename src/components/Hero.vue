<template>
    <section class="relative h-dvh w-full bg-black overflow-hidden">

        <!-- Grille en 3 colonnes -->
        <div class="absolute inset-0 z-10 grid grid-cols-3 place-items-center px-4 md:px-16 text-white">

            <!-- Colonne 1 : Texte gauche -->
            <div
                class="font-inter uppercase text-center text-sm md:text-lg leading-tight font-light tracking-wider -translate-y-12 opacity-0 animate-fade-in-delayed-1">
                Photographe<br />Indépendant
            </div>

            <!-- Colonne 2 : Image centrale -->
            <div>
                <img :src="heroImage" alt="Hero Image"
                    class="w-[250px] md:w-[330px] object-contain opacity-0 animate-fade-in-up" />
            </div>

            <!-- Colonne 3 : Texte droite -->
            <div
                class="font-inter uppercase text-center text-sm md:text-lg leading-tight font-light tracking-wider -translate-y-12 opacity-0 animate-fade-in-delayed-1">
                Basé à<br />Lyon
            </div>
        </div>

        <!-- Nom centré bas -->
        <div
            class="absolute bottom-6 left-1/2 transform -translate-x-1/2 z-10 opacity-0 animate-slide-in-right-delayed">

            <h1 class="text-white uppercase custom-title">
                Sharp Glint
            </h1>
        </div>
    </section>
</template>

<script setup>
import heroImage from '@/assets/hero.png'
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

/* Animations */
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

.animate-fade-in-delayed-2 {
    animation: fadeIn 1s ease-out 1.5s forwards;
}

@keyframes slideInRight {
    0% {
        opacity: 0;
        transform: translateX(100%);
    }

    100% {
        opacity: 1;
        transform: translateX(0);
    }
}

.animate-slide-in-right-delayed {
    animation: slideInRight 1s ease-out 1.5s forwards;
}
</style>