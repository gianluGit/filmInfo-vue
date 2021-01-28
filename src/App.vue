<template>
  <div id="app">
    <Navbar v-on:inputData="updateInput($event)" />
    <Jumbo />
    <h1 class="title-section">Film</h1>
    <GetFilms v-bind:input="searchedData" />
    <h1 class="title-section">Serie Tv</h1>
    <GetSeries v-bind:input="searchedData" />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Jumbo from './components/Jumbo.vue'
import GetFilms from './components/GetFilms.vue'
import GetSeries from './components/GetSeries.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    Jumbo,
    GetFilms,
    GetSeries
  },

  data: function() {
    return {
      searchedData: ""
    }
  },

  methods: {
    updateInput: function(searchedVal) {
      return this.searchedData = searchedVal;
    }
  }

}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  font-family: Avenir, Helvetica, Arial, sans-serif;

  body {
    background-color: #262626;

    h1.title-section {
      color: #fff;
      padding-left: 20px;
    }
  }

}
</style>
