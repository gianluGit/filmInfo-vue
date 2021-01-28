<template lang="html">
  <div id="jumbo">
    <div @click="next" class="arrow-right">
      <i class="fas fa-angle-right"></i>
    </div>

    <div @click="prev" class="arrow-left">
      <i class="fas fa-angle-left"></i>
    </div>

    <transition-group name="slide-fade" tag="div">
      <div v-for="i in [currentIndex]" :key="i" class="carousel">
        <img :src="currentImg" />
      </div>
    </transition-group>

  </div>
</template>

<script>
export default {
  name: 'Jumbo',
  components: {
  },

  data: function() {
    return {
      imgs: [
        require("../assets/sw.jpg"),
        require("../assets/up.jpg"),
        require("../assets/hp.jpg"),
        require("../assets/endgame.jpg"),
        require("../assets/soul.jpg")

      ],

      timer: null,
      currentIndex: 0
    };
  },

  mounted: function() {
    this.startSlide();

  },

  methods: {

    startSlide: function() {
      // this.timer = setInterval(this.next, 4000);
    },

    next: function() {
      this.currentIndex += 1;
      console.log(this.currentIndex);
    },

    prev: function() {
      this.currentIndex -= 1;
    }

  },

  computed: {
    currentImg: function() {
      return this.imgs[Math.abs(this.currentIndex) % this.imgs.length];

    }
  }
}
</script>

<style lang="scss" scoped>

  @media screen and (max-width: 800px) {
    .arrow-right, .arrow-left {
      display: none;
    }
  }

  #jumbo {
    height: 700px;
    position: relative;
    margin-bottom: 50px;
    margin-top: 85px;


    .arrow-right, .arrow-left {
      color: #fff;
      font-size: 60px;
      cursor: pointer;

      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      z-index: 600;
    }

    .arrow-right {
      right: 5%;
    }

    .arrow-left {
      left: 5%;
    }

    .carousel {
      height: 100%;

      img {
        width: 100%;
        height: 700px;
        border: 3px groove #cecece;
        border-radius: 8px;
      }
    }


    .slide-fade-enter-active {
      transition: all .8s ease;
    }

    .slide-fade-enter, .slide-fade-leave-to {
      transform: translateX(20px);
      opacity: 0;
    }

  }
</style>
