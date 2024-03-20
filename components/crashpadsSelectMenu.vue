<template>
    <div class="crashpad-box dark-box" @click="selectCrashpad">

      <div class="crashpad-image">
        <img alt="Crashpad Image" :src="imageSrc"/>
      </div>
      <div class="crash-description">
        <h3>{{ name }}</h3>
        <p>{{ description }}</p>
        <p>Price: ${{ price }}/day</p>
        <p v-if="selected">Selected!</p>
        <IconButton>Rent!</IconButton>
      </div>
    </div>
  </template>
  
  <script>

  export default {
    props: {
      name: String,
      description: String,
      price: Number,
      selected: Boolean,
      imageSrc: String
    },
    methods: {
      selectCrashpad() {
        console.log("hi")
      }
    }
  };
  </script>
  
  <style scoped lang="scss">

    .crashpad-box {
      border: 1px solid #ccc;
      cursor: pointer;
      width: 100%;
      display: flex;
      flex-direction: column;


      .crashpad-image {
        height: 20rem;
        position: relative;
        background-color: white;
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
        justify-content: center;
        

        img {
          height: 90%; 
        }
      }
      
      .crash-description {
        padding: 10px;
        overflow: auto;
        max-height: 10rem;
      }
    }

    .selected {
      color: blue;
      background-color: aqua;
    }
  

  </style>
  