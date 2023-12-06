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
  
<style>

  
.dark-box {
    background-color: rgb(40, 40, 40, 0.9);
    border-radius: 20px;
    border: 2px violet solid;
    margin: 5vh 0vw 5vh 0vw;
    box-shadow: -30px 40px 45px rgba(0, 0, 0, 1);
    color: ghostwhite;
    overflow: hidden;


    @media screen and (max-width: 467px) {
        width: 98vw;
        box-shadow: 0 0 0 black;
    }
}

.white-box {
    background-color: rgba(14, 14, 14, 0.9);
    border-radius: 20px;
    border: 2px ghostwhite solid;
    margin: 5vh 0vw 5vh 0vw;
    box-shadow: 0px 0px 10px 0px rgb(110, 100, 100);
    color: ghostwhite;
    overflow: hidden;


    @media screen and (max-width: 467px) {
        width: 98vw;
        box-shadow: 0 0 0 black;
    }
}

</style>