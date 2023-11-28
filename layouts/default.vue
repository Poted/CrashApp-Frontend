<template>
    <div>
      
      <!-- <FloatingButton /> -->
      <FloatingPointer class="absolute"/>
      <!-- </FloatingPointer> -->
      
      <!-- </FloatingPointer> -->
        <slot></slot>
      <!-- <nuxt /> -->
      <!-- <Footer /> -->
    </div>
  </template>
  
  <script>
  import FloatingPointer from '../components/floatingPointer.vue';
// import { FloatingButton } from '../components/floatingButton.vue';

//   import Footer from '~/components/Footer.vue';
  
  export default {
    components: {
      FloatingPointer,
    //   Footer,
    },
  };
  </script>
  