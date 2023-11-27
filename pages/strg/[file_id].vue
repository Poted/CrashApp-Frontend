<template>
    <div class="container flex flex-col items-center justify-center h-screen sm:w-full w-fit dark-box">

        <img class="img mb-8 rounded-md border-4" ref="image" :src="blobUrl" @load="loaded" />

        <div class="data-form grid grid-cols-12 gap-4 md:w-5/6 p-5 rounded-md border-2">

                <label class="col-span-3">ID: </label>
                <textarea readonly class="col-span-9" style="cursor: default;">{{ data.id }}</textarea>


                <label class="col-span-3">Size: </label>
                <label readonly class="col-span-9" style="cursor: default;">{{ data.size }}</label>
                

                <label class="col-span-3">Name: </label>
                <textarea class="col-span-9" style="cursor: pointer" type="text" v-model="data.name"></textarea>

                
                <label class="col-span-3">Directory: </label>
                <textarea class="col-span-9" style="cursor: pointer" type="text" v-model="data.directory"></textarea>

        </div>  

        <div class="flex flex-row mt-5 sm:mt-10">
            <ShineButton @click="saveChanges" text="Save" class="m-2 sm:mx-20"/>
            <nuxt-link to="/strg"  class="m-2 sm:mx-20">
                <ShineButton text="Back"/>
            </nuxt-link>
            
        </div>
        <nuxt-link @dblclick="handleDblClick">
            <DeleteButton @dblclick=" deleteFile(data.id)" />
        </nuxt-link>

    </div>
</template>


<script>
// import type { NuxtLink } from "#build/components"
import axios from "axios"
// import { deleteFile } from "~/pages/strg/index.vue"


// Load an image url as a blob
async function load(src) {
    const config = { url: src, method: "get", responseType: "blob" }
    const response = await axios.request(config)
    return response.data // the blob
}

/*  Loads the image as a blob and createObjectURL().
Set the img tag's src to the object url.
Once the image is loaded, revoke the object url (avoid memory leak).
Notice that the page can still show the image, but the src blob is no longer valid. */
export default {

    data() {
        const { file_id } = useRoute().params;
        return {
            blobUrl: ('http://localhost:80/getFile/' + file_id),
            data: {
                id: file_id,
                name: '',
                size: 0,
                directory: '',
            },
            formFields: [
                { key: "name", label: "Name" },
                { key: "size", label: "Size" },
                { key: "directory", label: "Directory" },
            ]
        };
    },
    props: {
        src: {
            type: String,
        },
    },

    methods: {

        loaded() {
            if (this.blobUrl)
                URL.revokeObjectURL(this.blobUrl);
        },

        async getData() {
            try {
                const response = await axios.get(`http://localhost:80/getFileData/` + this.data.id);
                this.data = response.data;
                if (response.status === 200) {
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

        async saveChanges() {
            try {

                const response = await axios.patch(`http://localhost:80/updateFile/${this.data.id}`, this.data);
                if (response.status === 200) {
                    console.log('Data updated successfully');
                }
                else {
                    console.error('Failed to update data');
                }
            }
            catch (error) {
                console.error('An error occurred while updating data:', error);
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

        handleDblClick() {
            this.$router.push('/strg')
        }

    },

    mounted() {
        this.getData();
    },
    // watch: {
    //     src: {
    //         immediate: true,
    //         handler(src) {
    //             if (!src)
    //                 return;
    //             load(src).then(blob => {
    //                 this.blobUrl = URL.createObjectURL(blob);
    //             });
    //         },
    //     },
    // },
    components: {} 
        // NuxtLink }
}
</script>


<style lang="scss">

.container {    


    // background-color: rgb(41, 39, 39, 0.7);
    // margin: 2vh 0 0 0;
    height: 90vh;
    // width: 70vw;
    // overflow: hidden;

    img {
        max-height: 500px;    
    }

    .data-form {
        background-color: rgb(41, 39, 39);

        label, textarea, input {
            background-color: rgb(72, 69, 69);
            height: 2.5vh;
            min-height: 2.5vh;
            max-height: 150px;
            margin: 0 0 1vh 0;
            font-weight: 500;
            color: rgb(233, 233, 233);
            text-align: center;
            overflow: hidden;

            
        }
        
        
    }

    @media screen and (max-width: 400px) {
        font-size: 9px;
        // width: 50%;
    }

    @media screen and (max-width: 640px) {
        font-size: 12px;
    }
}

</style>