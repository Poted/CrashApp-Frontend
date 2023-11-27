<template>
    <div class="floating-component">
        <div class="floating-point justify-end">
            <nuxt-link :to="'/'">
                <img @click="scrollToTop" ref="image" :src="blobUrl" @load="loaded" />
            </nuxt-link>
        </div>
    </div>
</template>
  
<script>
import axios from "axios"

export default {

    data() {
        const { file_id } = useRoute().params;
        return {
            blobUrl: ('http://localhost:80/getFile/' + 'b03767fd-a361-47e3-912a-3d386f31ec8d'),
        }
    },

    methods: {
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

        scrollToTop() {
            window.scrollTo({
                top: 0,
                behavior: 'smooth',
            });
        },
    }
}
</script>

<style scoped lang="scss">
.floating-component {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 0.5px;
    align-items: center;
    // background-color: #333;
    // color: white;
    padding: 10px;
    z-index: 1000;

    .floating-point {
        margin: 0 0 0 -1vw;
        // background-color: aqua;
        width: 8vw;

        // @media screen and (max-width: 646px) {
        //     margin: 85vh 0 0 0;
        // }

        @media (max-height: 400px) {
            margin: -13vh 0vw 0 -1vw;
            width: 12vw;
        }

        @media (max-width: 768px) {
            width: 30vw;
        }

        /* For tablet screens with a width between 768px and 1199px */
        @media (min-width: 768px) and (max-width: 1199px) {
            width: 12vw;
        }
    }


}
</style>
  