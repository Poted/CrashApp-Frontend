<template>
    <div class="landing-page p-0">
        <section class="hero flex flex-col">
            <div class="container dark-box flex flex-col items-center justify-center ">
                <h1 class="text-5xl font-bold text-center m-2">CrashApp</h1>
                <p class="text-lg text-center text-gray-500 mb-32">Your one-stop shop for all things bouldering.</p>
                <a href="/findYourCrashpad"><ShineButton class="m-2" text="Find yourself a crashpad"/></a>
                <!-- <nuxt-link to="/findYourCrashpad" exact><ShineButton class="m-2" text="Find yourself a crashpad"/></nuxt-link> -->
                <!-- <nuxt-link :to="'/findYourCrashpad'"><ShineButton class="m-2" text="Find yourself a crashpad"/></nuxt-link> -->
                <!-- <nuxt-link :to="'/findYourCrashpad'">
                    <ShineButton class="m-2" text="Find yourself a crashpad"/>
                </nuxt-link>
                <nuxt-link :to="'/findYourCrashpad'">
                    <ShineButton class="m-2" text="Find yourself a crashpad"/>
                </nuxt-link> -->
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

        <section class="call-to-action">
            <div class="container dark-box mx-auto flex flex-col items-center justify-center h-screen">
                <h2 class="text-5xl font-bold text-center">Get started today!</h2>
                <p class="text-lg text-center text-gray-500">Sign up for a free account and start climbing.</p>
                <a href="/register" class="btn btn-primary">Sign Up</a>
            </div>
        </section>
    </div>
</template>
  
<style lang="scss">

.dark-box {
        background-color: rgb(40, 40, 40, 0.9);
        border-radius: 20px;
        border: 2px violet solid;
        margin: 5vh 0vw 5vh 0vw;
        box-shadow: -30px 40px 45px rgba(0, 0, 0, 1);
        color: ghostwhite;
        overflow: hidden;


        @media screen and (max-width: 467px) { 
            width: 98vw;
            box-shadow: 0 0 0 black;
        }
}


.landing-page {

    // align-items: center;
    .hero {
            
    }
    
    .container {
        height: 90vh;

    }

    .features {
        // padding: 2rem;
    }

    .testimonials {
        // padding: 2rem;
    }

    .call-to-action {
        background-color: transparent;
        color: #fff;
    }

}
@media (min-width: 1200px) {
    body {
        background-position-y: -125px;
    }
}



body {
    background-image: url(../public/1328245.jpeg);
    background-position: center;
    background-position-y: -125px;
    background-attachment: fixed;

    display: flex;
    flex-direction: column;
    align-items: center;
}

/* For desktop screens with a width of 1200px or more */
@media (min-width: 1200px) {
    body {
        background-position-y: -125px;
    }
}

/* For tablet screens with a width between 768px and 1199px */
@media (min-width: 768px) and (max-width: 1199px) {
    body {
        background-position-y: -40px;
        // background-position-x: 169vh;
        background-size: 230vh;
    }
}

@media (max-width: 768px) {
    body {
        background-position-y: -20px;
        background-position-x: -9vh;
        background-size: 200vh;
    }
}

/* For mobile screens with a width less than 768px */
@media (max-width: 467px) {
    body {
        background-position-y: -40px;
        background-position-x: 169vh;
        background-size: 200vh;
    }
}
</style>