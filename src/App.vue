<template>
  <div id="app">
    <FlixHeader @search="startSearch" />
  </div>
</template>

<script>
import FlixHeader from "./components/FlixHeader.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    FlixHeader,
  },
  data() {
    return {
      movieFound: [],
      seriesFound: [],

      // allGeners: [],

      genresFound: "",
      apiKey: "3fcf4a781e2ec238aae1da6edb339733",
      language: "it-IT",
    };
  },

  methods: {
    // Funzione di ricerca
    startSearch(searchValue) {
      this.getMovie(searchValue);
      this.getTv(searchValue);
    },

    // Funzione di ricerca film
    getMovie(searchValue) {
      const params = {
        params: {
          api_key: this.apiKey,
          query: searchValue,
          language: this.language,
        },
      };

      axios
        .get("https://api.themoviedb.org/3/search/movie", params)
        .then((response) => {
          this.movieFound = response.data.results;

          console.log(this.movieFound);
        })
        .catch((error) => {
          console.log(error);
        });
    },

    // Funzione di ricerca serie TV
    getTv(searchValue) {
      const params = {
        params: {
          api_key: this.apiKey,
          query: searchValue,
          language: this.language,
        },
      };

      axios
        .get("https://api.themoviedb.org/3/search/tv", params)
        .then((response) => {
          this.seriesFound = response.data.results;

          console.log(this.seriesFound);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style lang="scss">
@import "./assets/style/common.scss";

body {
  background-image: url("../src/assets/img/netflix-image.jpg");
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center top;
}
</style>