<template>
  <div class="folder-modal" v-if="showFolderModal">
    <div class="folder-modal-content rounded-xl">
      <span class="close" @click="closeFolderModal">&times;</span>
      <!-- 
      <div v-for="photo in photosData" :key="photo.id">
        <label>hi</label>
        <img class="img m-8 rounded-md w-5/6" ref="image" :src="blobUrl + photo.id" @load="loaded" />
      </div> -->

      <div class="input-fields flex items-center w-full justify-around gap-4">
        <InputField v-model="inputFields" @input="handleDataFromInput" />
        <!-- <InputField  @input="handleDataFromInput" /> -->
        <!-- <InputField @input="$refs." /> -->
        
        <p>Value in ParentComponent: {{ this.inputFields.data  }}</p>
        <!-- <p>Value in ParentComponent: {{ this.$refs.inpField }}</p> -->
        
        
        <!-- <input v-model="message" placeholder="edit me" /> -->

        <ShineButton />
      </div>


    </div>
  </div>
</template>
  
<script>
import axios from "axios"
// import { InputField } from "@/components/inputField.vue";

export default {

  components: {
    // InputField,
  },
  
  data() {
    return {
      showFolderModal: false,
      inputValue: '',
      inputFields: '',

      photosData: [],
      blobUrl: ('http://localhost:80/getFile/'),
    };
  },

  methods: {

    handleDataFromInput(data) {
      // console.log(data)
      this.inputFields = data;
      console.log("W", this.inputFields)
    },

    // emitInputValue(event) {
    //   console.log(this.inputValue)
    //   this.$emit('input', this.inputValue);
    // },

    async getPhotosData() {
      try {
        const photosData = await axios.get(`http://localhost:80/filesList/`);
        this.photosData = photosData.data;
        if (photosData.status === 200) {
          console.log('Data fetched successfully');
        }
        else {
          console.error('Failed to fetch the data');
        }
      }
      catch (error) {
        console.error('An error occurred while fetching data:', error);
      }

    },


    openFolderModal() {
      this.showFolderModal = true;
      document.addEventListener('keydown', this.closeModalOnEscape);
    },

    closeFolderModal() {
      this.showFolderModal = false;
      document.removeEventListener('keydown', this.closeModalOnEscape);
    },

    closeModalOnEscape(event) {
      if (event.key === 'Escape') {
        this.closeFolderModal();
      }
    },

    // updateInputValue(value) {
    //   this.$refs.emitInputValue = value;
    // },

    // getInputValue() {
    //   this.inputFields = this.inputFields.emitInputValue;
    // },

  },

  mounted() {
    this.getPhotosData();
  },

  




};
</script>
  
<style>
.folder-modal {
  position: fixed;
  z-index: 1;
  background-color: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
  overflow: auto;
  left: 0;
  top: 0;
}

.folder-modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 40%;

  @media (max-width: 768px) {
    margin: 35% auto;
    width: 80%;
  }

  .input-fields {
    /* margin: -80px 0 0 0; */
  }

}

.close {
  color: #aaa;
  float: right;
  font-size: 32px;
  font-weight: bold;
  margin: -25px -10px 0 0;
  text-align: right;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>
  