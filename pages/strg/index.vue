<template>
    <div class="flex flex-col items-center">

        <div class="buttons flex md:mb-8">
            <ShineButton class="flex-1 sm:mt-24 mt-32 sm:-mb-10 m-3" 
                                @click="openModal" text="Upload Photo" />
            <PhotoUploadModal ref="addFileModal"/>
            
            <ShineButton class="flex-1 text-right w-48 sm:mt-24 mt-32 sm:-mb-10 m-3"
                                @click="openFolderModal" text="Folders" />
            <FolderUploadModal ref="addFolderModal" />

        </div>

        <NoData v-if="photosData == 0" class="noDataStrg"/>
        <div v-else class="grid grid-cols-2 sm:grid-cols-4 gap-1 sm:gap-4 m-4 p-0 sm:p-10">
            <div class="content h-60 h-full flex flex-col items-center justify-end rounded-xl text-white border-2 p-5 overflow-hidden"
                v-for="photo in photosData" :key="photo.id">

                <div class="flex flex-col items-center justify-center max-w-fit">
                    <img class="img m-8 rounded-md w-5/6" ref="image" :src="blobUrl + photo.id" @load="loaded" />
                    <div style="overflow: hidden;
                                text-overflow: ellipsis; 
                                white-space: unset; 
                                max-height: 50px;
                                max-width: 80%;
                            ">
                        {{ photo.name }}
                    </div>
                    <hr style="text:ghostwhite; width: 100%; margin: 1vh 0 0 0;" />

                </div>
                <div class="flex sm:flex-row flex-col gap-1 justify-between sm:items-end items-center w-full">
                    <nuxt-link :to="`/strg/` + photo.id" class="mt-4 col-span-2">
                        <ShineButton text="Edit" />
                    </nuxt-link>
                    
                    <DeleteButton @dblclick="deleteFile(photo.id); getPhotosData()" class="col-span-8"/>
                </div>

            </div>

        </div>

    </div>
</template>

<script>
import axios from "axios"
import PhotoUploadModal from '@/components/addFileModal.vue';
import FolderUploadModal from '@/components/addFolderModal.vue';



export default {

    data() {
        return {
            photosData: [],
            blobUrl: ('http://localhost:80/file/'),
        }
    },

    methods: {

        async getPhotosData() {

            try {
                const photosData = await axios.get(`http://localhost:80/filesList/018f8db8-56f1-7805-95f0-3899f0732fc0`);
                this.photosData = photosData.data;
                console.log("this.photosData")
                console.log(this.photosData.data[0])
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

        async deleteFile(id) {
            try {

                const response = await axios.delete(`http://localhost:80/deleteFile/${id}`);
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
        },

        openModal() {
            this.$refs.addFileModal.openModal()
        },
        
        openFolderModal() {
            this.$refs.addFolderModal.openFolderModal()
        },

    },

    components: {
        PhotoUploadModal,
        FolderUploadModal,
    },

    mounted() {
        this.getPhotosData();
    },

}
</script>

<style lang="scss">
.content {
    background-color: rgb(40, 40, 40, 0.8);

    
    img {
        max-height: 500px;
    }
}

.buttons {   
        button {
            min-height: 100%;
            width: 100%;
        }
}

.noDataStrg {
    // margin: 5vh 0 15vh 0;
    // padding: 20vh 10vw 20vh 10vw;
    height: 60vh;
    margin: 5vh 0 0 0;
}
</style>