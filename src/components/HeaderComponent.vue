<template>
  <header>
    <nav id="nav-back" class="flex pt-6 w-full lg:w-5/6 mx-auto">
      <div class="flex justify-center w-full">
        <div class="title-page-container">
          <h1 ref="title" class="title-page-text text-color transition-all duration-500 text-xl heading">{{ pageTitle }}</h1>
          <div ref="underline" class="title-page-underline bg-secondary-color h-0.5 bg-slate-900"></div>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
import { gsap } from 'gsap';

export default {
  name: 'HeaderComponent',
  props: {
    pageTitle: {
      type: String,
      required: true
    }
  },
  mounted() {
    // Usa Vue.nextTick per assicurarti che il DOM sia completamente aggiornato prima di animare
    this.$nextTick(() => {
      if (this.$refs.underline && this.$refs.title) {
        // Animazione GSAP per la linea sottolineata
        gsap.fromTo(this.$refs.underline, 
          { opacity: 0, width: '0%' }, // Stato iniziale
          { opacity: 1, width: '100%', duration: 1, ease: 'power2.out' } // Stato finale
        );
        gsap.fromTo(this.$refs.title, 
          { opacity: 0 }, // Stato iniziale (numero)
          { opacity: 1, duration: 1, ease: 'power2.out' } // Stato finale (numero)
        );
      } else {
        console.warn("GSAP target elements 'underline' or 'title' are null.");
      }
    });
  }
};
</script>

<style scoped>
.title-page-underline {
  width: 0; 
}
.title-page-text {
  opacity: 0;
}
</style>
