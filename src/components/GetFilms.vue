<template lang="html">

  <div class="films-wrapper">
    <div class="films-container">

      <div v-on:click="scrollR" class="arrow-right">
        <i class="fas fa-angle-right"></i>
      </div>

      <div v-on:click="scrollL" class="arrow-left">
        <i class="fas fa-angle-left"></i>
      </div>

      <div v-for="(movie, idz) in movies" v-bind:key='idz' class="apiCall">
        <div v-if="movie.poster_path" class="poster-container">
          <img :src="poster + movie.poster_path" alt="poster_path">
        </div>
      </div>
    </div>
  </div>



</template>

<script>
import axios from 'axios';

export default {
  name: 'GetFilms',
  props: {
    input: {
      type: String
    }
  },
  data: function() {
    return {
      movies: [],
      poster: 'https://image.tmdb.org/t/p/w342',

      scrollAmount: 0,

      query: ['disney', 'marvel', 'lego', 'star wars', 'pixar', 'dreamworks']

    }
  },

  methods: {

    scrollR: function() {
      let filmsR = document.querySelector(".films-container");
      filmsR.scrollTo({
        top: 0,
        left: this.scrollAmount += 560,
        behavior: 'smooth'
      });

    },

    scrollL: function() {
      let filmsL = document.querySelector(".films-container");
      filmsL.scrollTo({
        top: 0,
        left: this.scrollAmount -= 560,
        behavior: 'smooth'
      });
    }

  },

  watch: {
    input: function() {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=13905809c368b789098db62d2afec412&query=${this.input}`)
        .then(res => {
          this.movies = res.data.results
        })
        .catch(err => console.log('err', err));
    }
  },



  mounted: function() {
    axios.get(`https://api.themoviedb.org/3/search/movie?api_key=13905809c368b789098db62d2afec412&query=${this.query[Math.floor(Math.random() * this.query.length)]}`)
      .then(res => {
        this.movies = res.data.results
        console.log(this.movies)
      })
      .catch(err => console.log('err', err));



  }


}

</script>

<style lang="scss" scoped>

  @media screen and (min-width: 1025px) {
    .poster-container:hover {
      transform: scale(1.1);

    }

  }


  .films-wrapper {
    position: relative;

    .films-container {

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
        display: flex;
        align-items: center;
        height: 400px;
        width: 50px;


      }

      .arrow-right {
        right: 0;
        justify-content: flex-start;
      }

      .arrow-left {
        left: 0;
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

    }
  }
</style>
