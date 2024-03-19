<template>
  <!-- <div class="crashpads-container"> -->
  <div class="crashpads-container grid md:grid-cols-4 grid-cols-1 gap-2 sm:gap-8">

    <CrashpadsSelectMenu
      v-for="(crashpad, index) in crashpads"
      :key="index"
      :name="crashpad.name"
      :description="crashpad.description"
      :price="crashpad.price"
      :selected="crashpad.selected"
      :image-src="crashpad.imageSrc"
    />
  
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
        crashpads: [
          { name: 'Crashpad 1', description: 'Description 1', price: 50, selected: false, imageSrc: 'https://travelito.pl/images/crashpad-ocun-moonwalk-02.jpg' },
          { name: 'Crashpad 2', description: 'Description 2', price: 60, selected: true, imageSrc: 'https://travelito.pl/images/crashpad-ocun-moonwalk-02.jpg' },
          { name: 'Crashpad 3', description: 'Description 3', price: 70, selected: false, imageSrc: 'https://www.polarsport.pl/media/catalog/product/cache/ed1dd25b44ac74c9dca085c463c89987/c/r/crashpad-la-sportiva-laspo-01.jpg' },
          { name: 'Crashpad 4', description: 'Description 4', price: 80, selected: true, imageSrc: 'https://www.polarsport.pl/media/catalog/product/cache/ed1dd25b44ac74c9dca085c463c89987/c/r/crashpad-la-sportiva-laspo-01.jpg' },
          { name: 'Crashpad 5', description: 'Description 5', price: 90, selected: false, imageSrc: 'https://8a.pl/media/catalog/product/c/r/crash_pad_ocun_moonwalk_fts_green_1643103566_72f6.jpg' },
          { name: 'Crashpad 6', description: 'Description 6', price: 100, selected: true, imageSrc: 'https://8a.pl/media/catalog/product/c/r/crash_pad_ocun_moonwalk_fts_green_1643103566_72f6.jpg' },
          { name: 'Crashpad 7', description: 'Description 7', price: 110, selected: false, imageSrc: 'https://gatsklep.pl/9605-home_default/crashpad-cirro.jpg' },
          { name: 'Crashpad 8', description: 'Description 8Description 8Descriptionscription 8Description 8Descricription 8Description 8Descriptionscription 8Description 8Descricription 8Description 8Descriptionscription 8Description 8Descricription 8Description 8Descriptionscription 8Description 8Descricription 8Description 8Descriptionscription 8Description 8Descricription 8Description 8Descriptionscription 8Description 8Descricription 8Description 8Descriptionscription 8Description 8Descricription 8Description 8Descriptionscription 8Description 8Descricription 8Description 8Descriptionscription 8Description 8Descriptionscription 8Description 8Descriptionscription 8Description 8Descriptionscription 8Description 8Description 8Description 8Description 8Description 8dsdsads', price: 120, selected: true, imageSrc: 'https://gatsklep.pl/9605-home_default/crashpad-cirro.jpg' }
        ]

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
  
  <style scoped lang="scss">
  
  .crashpads-container {
    position: absolute;
    top: 10%;
    width: 80vw;
    transform: translateX(-50%);
      

  }
    </style>
  