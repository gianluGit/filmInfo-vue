<template lang="html">

  <div class="series-wrapper">

    <div class="series-container">
      <div v-on:click="scrollR" class="arrow-right">
        <i class="fas fa-angle-right"></i>
      </div>

      <div v-on:click="scrollL" class="arrow-left">
        <i class="fas fa-angle-left"></i>
      </div>

      <div v-for="(serie, idz) in series" :key='idz' class="apiCall">
        <div v-if="serie.poster_path" class="poster-container">
          <img :src="poster + serie.poster_path" alt="poster">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'GetSeries',
  props: {
    input: {
      type: String
    }
  },
  data: function() {
    return {
      series: [],
      poster: 'https://image.tmdb.org/t/p/w342',

      scrollAmount: 0,

      query: ['stranger', 'the office', 'disney', 'star wars']



    }
  },

  methods: {

    scrollR: function() {
      let seriesR = document.querySelector(".series-container");
      seriesR.scrollTo({
        top: 0,
        left: this.scrollAmount += 560,
        behavior: 'smooth'
      });

    },

    scrollL: function() {
      let seriesL = document.querySelector(".series-container");
      seriesL.scrollTo({
        top: 0,
        left: this.scrollAmount -= 560,
        behavior: 'smooth'
      });
    }

  },

  watch: {
    input: function() {
      axios.get(`https://api.themoviedb.org/3/search/tv?api_key=13905809c368b789098db62d2afec412&query=${this.input}`)
        .then(res => {
          this.series = res.data.results
        })
        .catch(err => console.log('err', err));
    }
  },



  mounted: function() {

    axios.get(`https://api.themoviedb.org/3/search/tv?api_key=13905809c368b789098db62d2afec412&query=${this.query[Math.floor(Math.random() * this.query.length)]}`)
      .then(res => {
        this.series = res.data.results
        console.log(this.series)
      })
      .catch(err => console.log('err', err));

  }


}
</script>

<style lang="scss" scoped>

  .series-wrapper {
    position: relative;

    .series-container {
      height: 450px;
      display: flex;
      align-items: center;
      overflow-x: hidden;
      margin: 50px 0;


      .arrow-right, .arrow-left {
        color: #fff;
        font-size: 60px;
        cursor: pointer;

        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        z-index: 600;

        background-color: rgba(0, 0, 0, 0.8);
        border-radius: 5px;
        height: 400px;
        display: flex;
        align-items: center;
        width: 50px;

      }

      .arrow-right {
        right: 0%;
        justify-content: flex-start;
      }

      .arrow-left {
        left: 0%;
        justify-content: flex-end;
      }

      .poster-container {
        height: 400px;
        width: 280px;
        transition: 0.3s;
        margin-right: 5px;


        img {
          height: 100%;
          width: 100%;
          border-radius: 5px;
        }

      }

      .poster-container:hover {
        transform: scale(1.1);

      }


    }
  }

</style>
