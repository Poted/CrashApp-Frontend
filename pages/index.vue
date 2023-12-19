<template>
    <div class="landing-page p-0">


        <section class="call-to-action">
            <div class="container dark-box mx-auto flex flex-col items-center justify-center h-screen">

                <div class="main-text" :class="{ 'fade-out': isChanged }" @click="changeContent">
                    <h2 class="text-5xl font-bold text-center">Get started today!</h2>
                    <p class="text-lg text-center text-gray-500">Find the stuff you like and start climbing</p>
                    <h1 class="text-center">
                        the way you like.
                    </h1>
                </div>

                <div class="items grid grid-cols-3 gap-2 sm:gap-8" :class="{ 'show-items': isChanged }">

                    <div class="item white-box bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500">
                        <h1>CrashRent</h1>
                        <img src="blob:url" alt="">
                    </div>

                    <div  v-for="photo in photosData" :key="photo.id">

                        <div class="item white-box">
                        <h1>Crashpads</h1>
                        <img src="blob:url" alt="">
                    </div>    
                        
                    </div>

                    
                    <div class="item white-box">
                        <h1>Chalkbags</h1>
                        <img src="blob:url" alt="">
                    </div>
                    <div class="item white-box">
                        <h1>Chalk</h1>
                        <img src="blob:url" alt="">
                    </div>
                    <div class="item white-box">
                        <h1>Climbing<br>Brushes</h1>
                        <img src="blob:url" alt="">
                    </div>
                    <div class="item white-box">
                        <h1>Bouldering<br>Crashpads</h1>
                        <img src="blob:url" alt="">
                    </div>
                    <div class="item white-box">
                        <h1>Climbing<br>Shoes</h1>
                        <img src="blob:url" alt="">
                    </div>
                </div>

            </div>
        </section>

        <section class="hero flex flex-col">
            <div class="container dark-box flex flex-col items-center justify-center ">
                <h1 class="text-5xl font-bold text-center m-2">CrashApp</h1>
                <p class="text-lg text-center text-gray-500 mb-32">Your one-stop shop for all things bouldering.</p>
                <a href="/findYourCrashpad">
                    <ShineButton class="m-2" text="Find yourself a crashpad" />
                </a>
            </div>
        </section>

        <section class="features p-0">
            <div class="container dark-box mx-auto">
                <h2 class="text-2xl font-bold text-center">Features</h2>
                <ul class="flex flex-wrap justify-center mt-4">
                    <li class="w-1/3 p-4">
                        <h3 class="text-xl font-bold">Find bouldering gyms</h3>
                        <p class="text-gray-500">Discover bouldering gyms and outdoor climbing spots near you.</p>
                    </li>
                    <li class="w-1/3 p-4">
                        <h3 class="text-xl font-bold">Track your progress</h3>
                        <p class="text-gray-500">Log your climbs and track your progress over time.</p>
                    </li>
                    <li class="w-1/3 p-4">
                        <h3 class="text-xl font-bold">Connect with others</h3>
                        <p class="text-gray-500">Connect with other bouldering enthusiasts and find climbing partners.</p>
                    </li>
                </ul>
            </div>
        </section>

        <section class="testimonials">
            <div class="container dark-box mx-auto">
                <h2 class="text-2xl font-bold text-center">Testimonials</h2>
                <div class="flex flex-wrap justify-center mt-4">
                    <div class="w-1/3 p-4">
                        <p class="text-gray-700">"This app has helped me become a better climber."</p>
                        <span class="text-gray-500">John Smith</span>
                    </div>
                    <div class="w-1/3 p-4">
                        <p class="text-gray-700">"I love using this app to find new bouldering spots."</p>
                        <span class="text-gray-500">Jane Doe</span>
                    </div>
                </div>
            </div>
        </section>

    </div>
</template>

<script>

export default {
    data() {
        return {
            isChanged: false,
            photosData: [],
            blobUrl: ('http://localhost:80/getFile/'),
        }
    },
    methods: {
        changeContent() {

            this.isChanged = !this.isChanged;
        },
    },

}
</script>
  
<style lang="scss">

.landing-page {

    .call-to-action {

        color: #fff;

        .container {

            .main-text {
                cursor: pointer;
                position: absolute;
            }

            .fade-out {
                animation: fadeOut 1s ease-out;
                visibility: hidden;

                @keyframes fadeOut {
                    from {
                        visibility: visible;
                    }

                    to {
                        opacity: 0;
                        color: violet;
                        font-size: xx-large;
                    }
                }
            }


            .items {
                opacity: 0.9;
                border-radius: 10px;
                visibility: hidden;
                justify-content: space-around;

                .item {
                    text-align: center;
                    border-radius: 10px;
                    margin: inherit;
                    height: 100%;
                    width: 100%;
                    padding: 1vw;
                    cursor: pointer;

                    display: flex;
                    flex-direction: column;
                    align-items: center;
                    justify-content: center;

                    h1 {
                        position: absolute;
                    }
                }
            }

            .show-items {
                visibility: visible;
                animation: placeItems .4s alternate;
                width: 96%;
                height: 89%;

                @keyframes placeItems {
                    from {
                        width: 0px;
                        height: 95%;
                        font-size: 0px;
                        margin: 0;
                    }

                    to {}

                }

                @keyframes showItems {
                    from {
                        visibility: hidden;
                        opacity: 0;
                    }

                    to {
                        visibility: visible;
                    }
                }

            }


        }

    }

    .hero {}

    .container {
        height: 90vh;

    }

    .features {}

    .testimonials {}



}

</style>