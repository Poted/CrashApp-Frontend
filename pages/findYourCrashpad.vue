<template>
    <div class="crashpad" @click="selectCrashpad">
      <img :src="image" alt="Crashpad Image" class="crashpad-image" />
      <h3>{{ name }}</h3>
      <p>{{ description }}</p>
      <p>Price: ${{ price }}/day</p>
      <p v-if="selected">Selected!</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      id: String,
      name: String,
      description: String,
      price: Number,
    },
    data() {
      return {
        selected: false,
      };
    },
    methods: {
      selectCrashpad() {
        this.selected = !this.selected;
        this.$emit('select-crashpad', this.id, this.selected);
      },
    },
  };
  </script>
  
  <style scoped>
  .crashpad {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px;
    cursor: pointer;
  }
  
  .crashpad-image {
    width: 100%;
    max-height: 150px;
    object-fit: cover;
  }
  
  .selected {
    background-color: #c1f0c1;
  }
  </style>
  