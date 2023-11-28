<template>
  <div class="circle-container">
    <div class="circle" @click="showOptions">
      <transition name="bounce">

        <div v-if="showContent" class="elements">

          <div v-for="(item, index) in items" :key="index" class="circle-item" :style="getItemStyle(index)">
            {{ item }}
          </div>
          
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // items: ['1', '2', '3', '4', '5'],
      items: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10'],
      showContent: false
    };
  },
  methods: {

    getItemStyle(index) {
      const totalItems = this.items.length;
      const angle = (360 / totalItems) * index - 45;
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
    }

  },
};

function calculatePosition(angle, radius) {
  const radians = (angle * Math.PI) / 450;
  console.log(radians)

  const x = Math.cos(radians) * parseInt(radius);
  const y = Math.sin(radians) * parseInt(radius);
  return { x: `${x}px`, y: `${y}px` };
}

</script>

<style scoped>
.circle-container {
  /* display: flex;
  align-items: center; */
  /* justify-content: center; */
  /* height: inherit; */
  height: 100px;
  width: 100px;
}

.circle {
  /* position: relative; */
  width: 100px;
  height: 100px;
  background-color: #f0f0f0;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.circle-item {
  position: absolute;
  width: 40px;
  height: 40px;
  background-color: #3498db;
  color: #ffffff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.circle-item span {
  display: inline-block;
  text-align: center;
}

.bounce-enter-active {
  animation: bounce-in .5s;
}
.bounce-leave-active {
  animation: bounce-in .5s reverse;
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


</style>
