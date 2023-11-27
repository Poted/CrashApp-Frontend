<!-- <template>
    <header :class="{ 'header-hidden': headerHidden }" id="main-header">
      <h1>My Website</h1>
    </header>
  </template>
  
  <script>
  export default {
    data() {
      return {
        prevScrollPos: 0,
        headerHidden: false,
      };
    },
    mounted() {
      window.addEventListener('scroll', this.handleScroll);
    },
    destroyed() {
      window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
      handleScroll() {
        const currentScrollPos = window.pageYOffset;
  
        if (this.prevScrollPos > currentScrollPos) {
          this.headerHidden = false;
        } else {
          this.headerHidden = true;
        }
  
        this.prevScrollPos = currentScrollPos;
      },
    },
  };
  </script>
  
  <style scoped lang="scss">
  #main-header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: #333;
    color: white;
    padding: 10px;
    transition: top 0.3s;
  }
  
  .header-hidden {
    top: -60px; /* Adjust the height of the header */
  }
  </style>
   -->