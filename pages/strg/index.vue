<template>
    <div class="flex flex-col items-center">

        <ShineButton class="mt-12" @click="openModal" text="Upload Photo" />
        <PhotoUploadModal ref="addFileModal" />

        <NoData class="noDataStrg" v-if="photosData === 0" />
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



export default {

    data() {
        return {
            photosData: [],
            blobUrl: ('http://localhost:80/getFile/'),
        }
    },

    methods: {

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

    },

    components: {
        PhotoUploadModal,
    },

    mounted() {
        this.getPhotosData();
    },
    watch() {
        this.getPhotosData();
    }

}
</script>

<style lang="scss">
.content {
    background-color: rgb(40, 40, 40, 0.8);

    img {
        max-height: 500px;
    }
}

.noDataStrg {
    margin: 5vh 0 15vh 0;
    padding: 20vh 10vw 20vh 10vw;
}
</style>