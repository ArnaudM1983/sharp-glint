<template>
    
    <div class="relative w-full h-screen overflow-hidden" @mousemove="handleMouseMove">
      <img
        v-for="(img, index) in images"
        :key="index"
        :src="img.src"
        :ref="el => imageRefs[index] = el"
        class="absolute object-cover opacity-70 pointer-events-none"
        :style="{
          width: img.baseStyle.width,
          height: img.baseStyle.height,
          top: img.baseStyle.top,
          left: img.baseStyle.left,
          position: 'absolute',
        }"
      />
      
      <div class="relative z-10 flex flex-col items-center justify-center h-full text-center fade-in-up">
        <h2 class="text-[10vw] text-white font-bold mb-4 uppercase">Sublimez Vos<br> Instants Simples</h2>
        <a href="" class="button text-white">Contactez-moi</a>
      </div>
    
    </div>
  </template>
  
  <script>
  import { gsap } from "gsap";
  import projet1 from '@/assets/projet1a.png';
  import projet2 from '@/assets/projet2a.png';
  import projet3 from '@/assets/projet3a.png';
  import projet4 from '@/assets/projet4a.png';
  import projet5 from '@/assets/projet5.png';

  
  export default {
    name: 'RandomImagesComponent',
    data() {
      return {
        images: [
          { src: projet1, baseStyle: { width: '250px', height: '250px', top: '10%', left: '5%' } },
          { src: projet2, baseStyle: { width: '220px', height: '220px', top: '5%', left: '80%' } },
          { src: projet3, baseStyle: { width: '350px', height: '350px', top: '60%', left: '10%' } },
          { src: projet4, baseStyle: { width: '250px', height: '250px', top: '70%', left: '65%' } },
        ],
        windowWidth: window.innerWidth,
        windowHeight: window.innerHeight,
        imageRefs: [], 
      };
    },
    methods: {
      handleMouseMove(event) {
        const mouseX = event.clientX;
        const mouseY = event.clientY;
  
        this.images.forEach((img, index) => {
          const intensity = 300 * (index + 1) / this.images.length; 
          const offsetX = ((mouseX / this.windowWidth) - 0.5) * intensity;
          const offsetY = ((mouseY / this.windowHeight) - 0.5) * intensity;
  
          gsap.to(this.imageRefs[index], {
            duration: 2,
            ease: "power3.out",
            x: offsetX,
            y: offsetY,
          });
        });
      }
    },
    mounted() {
      window.addEventListener('resize', () => {
        this.windowWidth = window.innerWidth;
        this.windowHeight = window.innerHeight;
      });
    },
    beforeUnmount() {
      window.removeEventListener('resize', () => {
        this.windowWidth = window.innerWidth;
        this.windowHeight = window.innerHeight;
      });
    },
  };

  
  </script>
  
  <style scoped>
  img {
    pointer-events: none;
    user-select: none;
  }
  
  @keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in-up {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.3s, transform 0.3s;
}

.fade-in-up.visible {
  animation: fadeInUp 1s ease-out forwards;
}


  </style>
  