<template lang="html">
  <div id="nav">
    <div class="lg-navbar">
      <div class="nav-container">
        <a id="page-title" href="#">FilmInfo</a>


        <div class="search">
          <input v-model="inputVal" id="main-search" type="text" name="" value="" placeholder="Cerca film o serie tv">
          <div v-on:click="startSearch()" class="searched">
            <i  class="fas fa-search"></i>
          </div>
        </div>


        <div class="links">
          <a href="#">Serie Tv</a>
          <a href="#">Film</a>
          <a href="#">Popolari</a>
        </div>


      </div>

    </div>

    <div class="xs-navbar">
      <div class="mobile-nav">
        <a href="#">FilmInfo</a>

        <div v-if="display" class="h-links">
          <a href="#">Film</a>
          <a href="#">Serie Tv</a>
          <a href="#">Popolari</a>
          <input type="text" name="" value="" placeholder="Cerca film o serie tv">
        </div>

        <div v-on:click="showMenu" class="hamburger">
          <i class="fas fa-bars"></i>
        </div>

      </div>

    </div>

  </div>
</template>

<script>
export default {
  name: 'Navbar',
  data: function() {
    return {

      display: false,
      inputVal: ''

    }
  },

  methods: {

    showMenu: function() {
      return this.display = !this.display;
    },

    startSearch: function() {
      this.$emit("inputData", this.inputVal);
      this.inputVal = "";
    }

  },
}
</script>

<style lang="scss" scoped>

  @media screen and (max-width: 1024px) {
    #nav .lg-navbar {
      display: none;
    }

  }


  @media screen and (min-width: 1025px) {
    .xs-navbar {
      display: none;
    }
  }


  #nav {
    height: 80px;
    background-color: #262626;
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 999;

    .lg-navbar{
      height: 100%;
    }

    .nav-container {
      display: flex;
      align-items: center;
      justify-content: space-between;

      height: 100%;
      padding: 0 20px;

      & > a#page-title {
        color: white;
        font-size: 40px;
        font-weight: bold;

      }

      .search {
        input#main-search {
          width: 300px;
          padding: 10px;
          background-color: #404040;
          border: none;
          outline: none;
          color: #fff;
        }

        .fa-search {
          margin-left: 20px;
          font-size: 20px;
          color: #fff;
          cursor: pointer;
        }

        .searched {
          display: inline-block;
        }

      }


      a {
        color: #fff;
        text-decoration: none;

      }

      .links {
        margin-left: 20px;

        & > a {
          margin-right: 20px;
          color: #cccccc;
          transition: 0.3s;

        }
        & > a:hover {
          color: #fff;
        }
      }

    }

    .xs-navbar {
      height: 250px;


      .mobile-nav {
        height: 100%;
        overflow: hidden;
        position: relative;

        & > a {
          text-decoration: none;
          color: white;
          font-size: 40px;
          font-weight: bold;
          padding: 0 20px;
          line-height: 80px;
        }

        .h-links {
          background-color: #262626;
          height: 100%;
          padding: 14px 20px;

          input {
            outline: none;
            padding: 5px;
            border: none;
            background-color: #404040;
            color: #fff;
            margin-top: 10px;
          }

          a {
            color: #cccccc;
            text-decoration: none;
            font-size: 22px;
            display: block;
            width: 100px;
            transition: 0.3s;
          }

          a:hover {
            color: #fff;
          }
        }

        .hamburger {
          font-size: 40px;
          color: white;
          position: absolute;
          top: 8px;
          right: 20px;
          cursor: pointer;

        }

      }
    }


  }
</style>
