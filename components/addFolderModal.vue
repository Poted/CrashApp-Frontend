<template>
  <div class="folder-modal" v-if="showFolderModal">
    <div class="folder-modal-content rounded-xl">
      <span class="close" @click="closeFolderModal">&times;</span>

      <div class="input-fields flex items-center w-full justify-around gap-4">
   
        <InputField @input="updateInputValue" />

        <p>Value in ParentComponent: {{ this.inputValue  }}</p>

        <ShineButton />
      </div>

    </div>
  </div>
</template>
  
<script>
import axios from "axios"

export default {

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

    updateInputValue(event) {
      this.inputValue = event.target.value;
    },

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

    addFolder() {
      
    }

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
   
    p {
      max-width: 10vw;
      overflow: hidden;
      word-break: break-all;
      white-space: normal;
      
    }
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
  