<template>
  <div class="modal flex flex-col items-center" v-if="showModal">
    <div class="modal-content rounded-xl m-24" @keydown.esc="closeModal">
      <span class="close" @click="closeModal">&times;</span>

      <div class="flex flex-col items-center mt-6">
        <label v-if="selectedFile" class="w-72 h-80 text-center cursor-pointer" for="fileInput">
          <img v-if="thumbnail" :src="thumbnail" alt="Thumbnail" class="w-full" />
          <span> {{ selectedFile.name }}</span>
        </label>
        <NoData v-else @click="$refs.fileInput.click()" class="cursor-pointer"/>
        <input id="fileInput" class="invisible" type="file" ref="fileInput" @change="handleFileChange" />

        <ShineButton v-if="selectedFile" @click="uploadPhoto" text="Upload Photo" class="m-2" />
        <ShineButton v-else @click="this.$refs.fileInput.click()" text="Upload Photo" class="m-2" />
      </div>
      <div>
        <div>
        </div>
      </div>
    </div>

  </div>
</template>
  
<script>
import axios from "axios"

export default {

  data() {
    const { folder_id } = useRoute().params;
    return {
      folder_id: folder_id,
      selectedFile: null,
      showModal: false,
      thumbnail: null,
      tmbnl: null
    };
  },

  methods: {

    handleFileChange(event) {

      this.selectedFile = event.target.files[0];

      const input = event.target;
      if (input.files && input.files[0]) {
        const reader = new FileReader();

        reader.onload = (e) => {
          // Create a thumbnail using canvas
          const img = new Image();
          img.src = e.target.result;

          const canvas = document.createElement('canvas');
          const ctx = canvas.getContext('2d');
          const maxThumbnailSize = 100; // Set your desired thumbnail size

          let width = img.width;
          let height = img.height;

          if (width > height) {
            if (width > maxThumbnailSize) {
              height *= maxThumbnailSize / width;
              width = maxThumbnailSize;
            }
          } else {
            if (height > maxThumbnailSize) {
              width *= maxThumbnailSize / height;
              height = maxThumbnailSize;
            }
          }

          canvas.width = width;
          canvas.height = height;
          ctx.drawImage(img, 0, 0, width, height);

          // Set the thumbnail data URL to be used in the img tag
          this.thumbnail = canvas.toDataURL('image/png');
        };

        reader.readAsDataURL(input.files[0]);
      }

    },

    uploadPhoto() {
      if (this.selectedFile) {
        this.addFile(this.selectedFile);
        this.closeModal();
      } else {
        console.error('No file selected');
      }
    },

    async addFile(body) {
      try {

        const formData = new FormData();

        formData.append('file_name', body)

        if (!this.folder_id) {
          this.folder_id = 1
        }
        
        const response = await axios.post(`http://localhost:80/saveFile/` + this.folder_id, formData);
        if (response.status === 201) {
          console.log('Added successfully');
        }
        else {
          console.error('Failed to upload a data');
        }
      }
      catch (error) {
        console.error('An error occurred while uploading data:', error);
      }
    },

    openModal() {
      this.showModal = true;
      document.addEventListener('keydown', this.closeModalOnEscape);
    },

    closeModal() {
      this.showModal = false;
      this.selectedFile = null;
      this.$emit('modal-closed');
      document.removeEventListener('keydown', this.closeModalOnEscape);
    },

    closeModalOnEscape(event) {
      if (event.key === 'Escape') {
        this.closeModal();
      }
    },

  },

  mounted() {
  },

  watch: {
    thumbnail(newVal, oldVal) {
      if (!oldVal && newVal) {
        console.log('\nthumbnail' + this.thumbnail)
      }
    }
  }

};
</script>
  
<style>
.modal {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-content {
  background-color: #fefefe;
  /* margin: 8% auto; */
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
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

img {
  max-height: 100%;
  object-fit: contain;
}
</style>
  