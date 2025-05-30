<template>
  <section id="contact">
    <div ref="container" class="relative w-full h-screen overflow-hidden" @pointermove="handleMouseMove">
      <img v-for="(img, index) in images" :key="index" :src="img.src" :ref="el => imageRefs[index] = el"
        class="absolute object-cover opacity-70 pointer-events-none" :style="{
          width: isMobile ? reduceSize(img.baseStyle.width) : img.baseStyle.width,
          height: isMobile ? reduceSize(img.baseStyle.height) : img.baseStyle.height,
          top: isMobile ? img.mobileStyle?.top || img.baseStyle.top : img.baseStyle.top,
          left: isMobile ? img.mobileStyle?.left || img.baseStyle.left : img.baseStyle.left,
          position: 'absolute',
        }" />

      <div ref="title" class="relative z-10 flex flex-col items-center justify-center h-full text-center">
        <h2 class="text-[18vw] md:text-[10vw] text-white font-bold mb-4 uppercase">
          Sublimez Vos<br /> Instants Simples
        </h2>
        <a href="" class="button text-white">Contactez-moi</a>
      </div>
    </div>
  </section>
</template>

<script>
import { gsap } from "gsap";
import projet1 from "@/assets/projet1a.png";
import projet2 from "@/assets/projet2a.png";
import projet3 from "@/assets/projet3a.png";
import projet4 from "@/assets/projet4a.png";

export default {
  name: "RandomImagesComponent",
  data() {
    return {
      images: [
        {
          src: projet1,
          baseStyle: { width: "250px", height: "250px", top: "10%", left: "5%" },
          mobileStyle: { top: "1%", left: "10%" }
        },
        {
          src: projet2,
          baseStyle: { width: "220px", height: "220px", top: "5%", left: "80%" },
          mobileStyle: { top: "10%", left: "70%" }
        },
        {
          src: projet3,
          baseStyle: { width: "350px", height: "350px", top: "60%", left: "10%" },
          mobileStyle: { top: "60%", left: "-20%" }
        },
        {
          src: projet4,
          baseStyle: { width: "250px", height: "250px", top: "70%", left: "65%" },
          mobileStyle: { top: "75%", left: "60%" }
        },
      ],

      windowWidth: window.innerWidth,
      windowHeight: window.innerHeight,
      imageRefs: [],
      animationPlayed: false,
      isMobile: window.innerWidth < 768,
    };
  },
  methods: {

    // Offset based on mouse position
    handleMouseMove(event) {
      const mouseX = event.clientX;
      const mouseY = event.clientY;

      this.images.forEach((img, index) => {
        const intensity = (300 * (index + 1)) / this.images.length;
        const offsetX = ((mouseX / this.windowWidth) - 0.5) * intensity;
        const offsetY = ((mouseY / this.windowHeight) - 0.5) * intensity;

        // Animate the image to the new position using GSAP
        gsap.to(this.imageRefs[index], {
          duration: 2,
          ease: "power3.out",
          x: offsetX,
          y: offsetY,
        });
      });
    },
    playAnimation() {
      if (this.animationPlayed) return;
      this.animationPlayed = true;

      // Animate the title section: fade in from the bottom
      gsap.from(this.$refs.title, {
        duration: 2.5,
        y: 100,
        opacity: 0,
        ease: "power3.out",
      });
    },
    handleResize() {
      this.windowWidth = window.innerWidth;
      this.windowHeight = window.innerHeight;
      this.isMobile = window.innerWidth < 768;
    },
    reduceSize(size) {
      const num = parseInt(size);
      return Math.round(num * 0.6) + "px"; 
    },
  },
  mounted() {
    window.addEventListener("resize", this.handleResize);

    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          this.playAnimation();
          observer.disconnect();
        }
      },
      { threshold: 0.3 }
    );

    observer.observe(this.$refs.container);
  },
  beforeUnmount() {
    window.removeEventListener("resize", this.handleResize);
  },
};
</script>

<style scoped>
img {
  pointer-events: none;
  user-select: none;
}
</style>
