<template>
  <div>
    <FloatingPointer class="absolute"/>
    <slot></slot>
    </div>
  </template>
  
<script>
  export default {

};
</script>
  
<style lang="scss">


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

.white-box {
    background-color: rgba(14, 14, 14, 0.9);
    border-radius: 20px;
    border: 2px ghostwhite solid;
    margin: 5vh 0vw 5vh 0vw;
    box-shadow: 0px 0px 10px 0px rgb(110, 100, 100);
    color: ghostwhite;
    overflow: hidden;


    @media screen and (max-width: 467px) {
        width: 98vw;
        box-shadow: 0 0 0 black;
    }
}

</style>