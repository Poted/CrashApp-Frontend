<template>

  <div class="menu-container">
    
    <div class="calendar-container">
      <Calendar/>
    </div>    

      <InputField class="input-field" label="Dzien dobry Pan Legoss!"/>
      <InputField class="input-field" label="Your name"/>
      <InputField class="input-field" label="City"/>
      <InputField class="input-field" label="ID"/>
      <PhoneInput class="input-field" />    

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
    
  };
  </script>
  
  <style scoped lang="scss">

 .menu-container {
   
   display: flex;
   flex-direction: column;
   width: 80vw;
   margin-top: 5vh;

   
  @media (max-width: 768px) {
    margin-top: 11vh;
    width: 95vw;
  }
  
  @media (max-width: 467px) {
    margin-top: 11vh;
  }

   
   .input-field {
      align-self: center;
      width: 40%;
      z-index: 1;
      background-color: rgba($color: #000000, $alpha: 0.7);
      border-radius: 20px;
      color: whitesmoke;
      font-size: large;

      @media (min-width: 768px) and (max-width: 1199px) {
        width: 80%;
      }

      @media (max-width: 768px) {
        width: 100%;
      }
    }


    .calendar-container {

      height: 45vh;
      display: flex;
      flex-direction: column;
      // margin-bottom: -5vh;
      
      @media (max-width: 768px) {
        margin-bottom: -5vh;
      }

      @media (min-width: 768px) and (max-width: 1199px) {
        height: 35vh;
      }
      
      .calendar {
        align-self: center;        
      }
    }  
    
    .crashpads-container {
      margin: 6vh 0 5vh 0;

      @media (max-width: 467px) {
        // width: 95%;
        align-self: center;
      }
    }
  }
    </style>
  