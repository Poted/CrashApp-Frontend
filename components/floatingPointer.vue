<template>
    <div class="floating-component">
        <div class="floating-point justify-end">

            <div class="circle-container">
                <img ref="image" @click="showOptions" :src="blobUrl" @load="loaded" />
                <div class="circle">


                    <transition name="bounce" @after-enter="startButtonAnimation">
                        <div v-if="showContent" class="elements">

                            <!-- <ItalicSearchBar v-if="isFirstItem" :animated="buttonAnimated" /> -->

                            <div v-for="(item, index) in iconNames" :key="index" class="circle-item"
                                :style="getItemStyle(index)">

                                <template v-if="index == 0">
                                    <nuxt-link @click="showContent = !showContent" :to="getIconHref(item.src)">
                                        <img :src="getIconSrc(item.name)" alt="i">
                                    </nuxt-link>
                                    <div>
                                        <ItalicSearchBar :animated="buttonAnimated" class="isb" />
                                    </div>
                                </template>
                                <template v-else-if="item.name == 'facebook'">
                                    <a @click="showContent = !showContent" href="https://www.facebook.com/" target="_blank">
                                        <img :src="getIconSrc(item.name)" alt="i">
                                    </a>
                                </template>
                                <template v-else-if="item.name == 'instagram'">
                                    <a @click="showContent = !showContent" href="https://www.instagram.com/"
                                        target="_blank">
                                        <img :src="getIconSrc(item.name)" alt="i">
                                    </a>
                                </template>
                                <template v-else>
                                    <nuxt-link @click="showContent = !showContent" :to="getIconHref(item.src)">
                                        <img :src="getIconSrc(item.name)" alt="i">
                                    </nuxt-link>
                                </template>

                            </div>

                        </div>
                    </transition>













                    <!-- <ItalicSearchBar class="w-96"/> -->
                    <!-- 
                    <transition name="bounce">
                        <div v-if="showContent" class="elements">

                            <div v-for="(item, index) in iconNames" :key="index" class="circle-item"
                                :style="getItemStyle(index)">

                                <nuxt-link @click="showContent = !showContent" :to="getIconHref(item.src)">
                                    <img :src="getIconSrc(item.name)" alt="i">
                                </nuxt-link>

                            </div>

                        </div>
                    </transition> -->
                </div>
            </div>

        </div>
    </div>
</template>
  
<script>
import axios from "axios"

export default {
    data() {
        return {

            blobUrl: ('http://localhost:80/getFile/' + 'b03767fd-a361-47e3-912a-3d386f31ec8d'),


            iconNames: [
                { name: 'home', src: '' },
                { name: 'boulder', src: 'findYourCrashpad' },
                { name: 'cloud', src: 'strg' },
                { name: 'msg', src: 'contact' },
                { name: 'facebook' },
                { name: 'instagram' }
            ],

            items: [, '2', '3', '4', '5', '6'],
            showContent: false,
            buttonAnimated: false,

        };
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

        getItemStyle(index) {
            const totalItems = this.items.length;
            const angle = (360 / totalItems) * index - 22;
            // const angle = (360 / totalItems) * index;
            const radius = '100px';
            const position = calculatePosition(angle, radius);
            return {
                left: position.x,
                top: position.y,
            };
        },

        showOptions() {
            this.showContent = !this.showContent
        },

        getIconSrc(iconName) {
            return `/${iconName}.ico`;
        },

        getIconHref(href) {
            return `/${href}`;
        },

        startButtonAnimation() {
            this.buttonAnimated = true;
        },

    },

    mounted() {

        this.$nextTick(() => {
            setTimeout(() => {
                this.animate = true;
            }, 2000);
        });


        // const currentUrl = window.location.href;
        // console.log(currentUrl);

    },

}

function calculatePosition(angle, radius) {
    const radians = (angle * Math.PI) / 450;
    console.log(radians)

    const x = Math.cos(radians) * parseInt(radius);
    const y = Math.sin(radians) * parseInt(radius);
    return { x: `${x}px`, y: `${y}px` };
}

</script>

<style scoped lang="scss">
.floating-component {

    top: 0;
    left: 0;
    width: 100%;
    height: 0.5px;
    align-items: center;
    padding: 10px;
    z-index: 20;



    .floating-point {
        margin: 0 0 0 1vw;
        width: 8vw;
        position: fixed;
        border-radius: 50%;



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


        .circle-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;


            img {
                z-index: 10;
                position: relative;
                cursor: pointer;

            }

            .circle {

                position: relative;
                background-color: #f0f0f0;
                border-radius: 50%;
                display: flex;
                align-items: center;
                justify-content: center;
                height: 1px;
                width: 1px;
                top: -4.7rem;
                left: -1rem;
                box-shadow: 15px 12px 70px 15px #3498db;


                .circle-item {
                    box-shadow: -3px -3px 20px -10px #3498db;
                    border: 2px rgb(15, 55, 61) solid;
                    position: absolute;
                    width: 40px;
                    height: 40px;
                    background-color: #3498db;
                    color: #ffffff;
                    border-radius: 50%;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    overflow: hidden;


                    img {
                        width: 1.8rem;
                    }

                    .isb {
                        position: fixed;
                        width: 27.5vw !important;
                        margin: 0vh 0 0 5vw;

                        @media screen and (max-width: 646px) {
                            width: 100% !important;
                            margin: 20vh 0 0 -35vw;
                        }

                    }

                }

                .circle-item span {
                    display: inline-block;
                    text-align: center;
                }

                .bounce-enter-active {
                    animation: bounce-in .4s;
                }

                .bounce-leave-active {
                    animation: bounce-in .4s reverse;
                }

                @keyframes bounce-in {
                    0% {
                        transform: scale(0);
                    }

                    50% {
                        transform: scale(1.5);
                    }

                    100% {
                        transform: scale(1);
                    }
                }




            }

        }
    }





}
</style>