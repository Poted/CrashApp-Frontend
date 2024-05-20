<template>
  <div class="folder-modal" v-if="showFolderModal">
    <div class="folder-modal-content rounded-xl">
      <span class="close" @click="closeFolderModal">&times;</span>

      <div>
        <h2>Names List:</h2>
        <!-- <nuxt-link :to="'/strg'">
          <div class="folder-name folder-name flex items-center justify-between">
            {{ 'Main' || 'No name available' }}
            <DeleteButton @dblclick=" deleteFolder(folder.id)" class="deleteBtn invisible"/>
          </div>
        </nuxt-link> -->

        <ul>
          <li v-for="(folder, index) in this.foldersData.data" :key="index">

            <nuxt-link :to="'/strg'" v-if="folder.name.toLowerCase() == 'main'">
              <div class="folder-name folder-name flex items-center justify-between">
                {{ 'Main' || 'No name available' }}
                <DeleteButton @dblclick=" deleteFolder(folder.id)" class="deleteBtn invisible" />
              </div>
            </nuxt-link>
            <div class="folder-name flex items-center justify-between" v-else>
              <nuxt-link :to="'/strg/f/' + folder.id" class="w-full">
                <div>
                  {{ folder.name || 'No name available' }}
                </div>
              </nuxt-link>
              <DeleteButton @dblclick=" deleteFolder(folder[0].id)" class="deleteBtn w-full" />
            </div>
          </li>
        </ul>
      </div>

      <div class="input-fields flex flex-col items-center w-full justify-around gap-1">

        <InputField @input="updateInputValue" ref="inputField"/>

        <p v-if="this.inputValue.length <= 29">Folder name: {{ this.inputValue }}</p>
        <p v-if="this.inputValue.length > 29">Folder name should contains less than 30 characters.</p>

      </div>
      <ShineButton text="create folder" @click="addFolder" />

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
      foldersData: {},
      currentFolder: '',
    };
  },

  methods: {

    updateInputValue(event) {
      this.inputValue = event.target.value;
    },

    async getFoldersData() {
      try {

        const foldersData = await axios.get(`http://localhost:80/foldersList/018f5016-2a02-71b0-9305-74ae1464e75a`, {
          headers: { "Access-Control-Allow-Origin": "*", 'Access-Control-Allow-Headers': '*', },
        });
        this.foldersData = foldersData.data;

        if (foldersData.status === 200 || foldersData.status === 201) {
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
      document.addEventListener('keydown', this.keyListeners);
    },

    closeFolderModal() {
      this.showFolderModal = false;
      document.removeEventListener('keydown', this.keyListeners);
    },

    keyListeners(event) {
      if (event.key === 'Escape') {
        this.closeFolderModal();
      }

      if (event.key === 'Enter') {
        this.addFolder()
      }
    },
    
    async addFolder() {

      
      const folderData = {
        name: this.inputValue
      }
      
      this.$refs.inputField.clearInputValue();
      this.inputValue = ''

      try {

        console.log("name: " + folderData + " xd")

        const response = await axios.post(`http://localhost:80/saveFolder`, folderData);
        if (response.status === 201) {
          console.log('Data updated successfully');

          this.getFoldersData();


        }
        else {
          console.error('Failed to update data');
        }
      }
      catch (error) {
        console.error('An error occurred while updating data:', error);
      }

    },

    async deleteFolder(id) {
    
      try {

        const response = await axios.delete(`http://localhost:80/DeleteFolder/${id}`);
        if (response.status === 204) {
          console.log('Deleted successfully');
        }
        else {
          console.error('Failed to delete data');
        }
      }
      catch (error) {
        console.error('An error occurred while deleting data:', error);
      }

      this.getFoldersData();
    },

  },

  mounted() {
    this.getFoldersData();
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
  width: 50%;

  @media (max-width: 768px) {
    margin: 35% auto;
    width: 95%;
  }

  .input-fields {

    p {
      margin: 1vw;
      word-break: break-all;
      white-space: normal;
    }
  }

  .folder-name {
    border: 1px solid black;
    border-radius: 15px;
    margin: 1vh 0 0 1vh;
    padding: 10px;
    width: 100%;
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
  