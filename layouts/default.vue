<template>
    <div>
      <FloatingPointer />
        <slot></slot>
      <!-- <nuxt /> -->
      <!-- <Footer /> -->
    </div>
  </template>
  
  <script>
  import FloatingPointer from '../components/floatingPointer.vue';
//   import Footer from '~/components/Footer.vue';
  
  export default {
    components: {
      FloatingPointer,
    //   Footer,
    },
  };
  </script>
  