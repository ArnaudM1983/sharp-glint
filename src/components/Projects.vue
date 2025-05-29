<template>
    <section ref="sectionRef" class="relative min-h-screen bg-black overflow-x-hidden isolate">
        <!-- H2 animé en fond -->
        <transition name="fade-slide" appear>
            <h2 v-if="showTitle"
                class="fixed top-1/2 left-0 -translate-y-1/2 text-[20vw] font-bebas font-black whitespace-nowrap text-zinc-600 pointer-events-none select-none z-0 pl-10">
                PROJETS.
            </h2>
        </transition>

        <!-- Contenu scrollable -->
        <div class="relative z-10 max-w-[1300px] mx-auto pt-40 flex flex-col mt-90 pb-100">

            <div v-for="(project, index) in projects" :key="index" :class="[
                'group relative w-full transition-transform duration-300 hover:scale-[1.03]',
                index % 2 === 0 ? 'self-start' : 'self-end'
            ]" :style="{
                maxWidth: getProjectWidth(index),
                height: getProjectHeight(index),
                marginTop:
                    index === 1 ? '-200px' :
                        index === 2 ? '280px' :
                            index === 3 ? '250px' :
                                index === 4 ? '180px' : '0'
            }">

                <!-- Titre -->
                <h3 class="text-zinc-400 text-lg font-normal text-left mb-6">
                    {{ project.title }}
                </h3>

                <!-- Image -->
                <img :src="project.image" :alt="project.name" class="w-full object-cover mb-6 z-0" />

                <!-- Nom -->
                <p class="text-white text-left font-medium mb-1 uppercase">
                    {{ project.name }}
                </p>

                <!-- Catégorie -->
                <p class="text-zinc-400 text-left uppercase">
                    / {{ project.category }}
                </p>
            </div>
        </div>
    </section>
</template>


<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import heroImg from '@/assets/hero.png'
import projet1a from '@/assets/projet1a.png'
import projet2a from '@/assets/projet2a.png'
import projet3a from '@/assets/projet3a.png'
import projet4a from '@/assets/projet4a.png'


const projects = [
    {
        title: '/01',
        name: 'Lignes d’Horizon',
        category: 'Architecture',
        image: projet1a
    },
    {
        title: '/02',
        name: 'Lumière Silencieuse',
        category: 'Photographie d’intérieur',
        image: projet2a
    },
    {
        title: '/03',
        name: 'Fragments de Nature',
        category: 'Nature morte contemporaine',
        image: projet3a
    },
    {
        title: '/04',
        name: 'Ligne & Respiration',
        category: 'Études de lumière et d’ombre',
        image: projet4a
    },
    {
        title: '/05',
        name: 'Textures Muettes',
        category: 'Matière & Détail',
        image: heroImg
    }
]

const sectionRef = ref(null)
const showTitle = ref(false)

let observer = null

onMounted(() => {
    observer = new IntersectionObserver(
        ([entry]) => {
            showTitle.value = entry.isIntersecting
        },
        {
            root: null,
            threshold: 0.15
        }
    )
    if (sectionRef.value) observer.observe(sectionRef.value)
})

onBeforeUnmount(() => {
    if (observer && sectionRef.value) observer.unobserve(sectionRef.value)
})

const getProjectWidth = (index) => {
    // Largeurs différentes 
    const widths = ['400px', '520px', '460px', '480px'];
    return widths[index % widths.length];
};

const getProjectHeight = (index) => {
    // Hauteurs différentes pour varier 
    const heights = ['auto', '350px', '400px', '370px'];
    return heights[index % heights.length];
};

</script>

<style scoped>
.fade-slide-enter-active,
.fade-slide-leave-active {
    transition: opacity 0.6s ease, transform 0.6s ease;
}

.fade-slide-enter-from,
.fade-slide-leave-to {
    opacity: 0;
    transform: translateX(-150px);
}

.fade-slide-enter-to,
.fade-slide-leave-from {
    opacity: 0.8;
    transform: translateX(0);
}
</style>