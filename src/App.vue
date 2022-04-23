<template>
  <div id="app">
    <FlixHeader
      @search="startSearch"
      @SelectionGenre="getSelection"
      :genre="allGenres"
    />
    <FlixMain
      :movie="movieFound"
      :series="seriesFound"
      :trendingMovies="trendingMovies"
      :trendingTv="trendingTv"
    />
  </div>
</template>

<script>
import FlixHeader from "./components/FlixHeader.vue";
import FlixMain from "./components/FlixMain.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    FlixHeader,
    FlixMain,
  },
  data() {
    return {
      movieFound: [],
      seriesFound: [],

      allGeners: [],

      selectedGenres: [],
      selectedMovies: [],

      genresFound: "",
      apiKey: "3fcf4a781e2ec238aae1da6edb339733",
      language: "it-IT",

      trendingMovies: [],
      trendingTv: [],
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

    //  Funzione di ricerca generi
    getSelection(selection) {
      this.selectedGenres = selection;
      console.log("Ho ricevuto:" + this.selectedGenres.name);
    },

    // Funzione di filtraggio generi
    loopGenres() {
      this.movieFound.forEach((element) => {
        console.log(element.genre_ids);
      });
    },
  },

  created() {
    //Funzione di cattura dei generi
    const paramsGenre = {
      params: {
        api_key: this.apiKey,
        language: this.language,
      },
    };
    axios
      .get("https://api.themoviedb.org/3/genre/movie/list", paramsGenre)
      .then((response) => (this.allGenres = response.data.genres));

    // Funzione per mostrare il trading
    axios
      .all([
        axios.get(
          "https://api.themoviedb.org/3/trending/movie/week?api_key=" +
            this.apiKey
        ),

        axios.get(
          "https://api.themoviedb.org/3/trending/tv/week?api_key=" + this.apiKey
        ),
      ])
      .then(
        axios.spread((resMovieT, resTV) => {
          this.trendingMovies = resMovieT.data.results;
          console.log("Trending", this.trendingMovies);
          this.trendingTv = resTV.data.results;
        })
      );
  },

  computed: {
    // getFilteredMovies() {
    //   this.movieFound = this.selectedMovies.filter((movie) =>
    //     movie.genre_ids.includes(this.selectedGenres.id)
    //   );
    // },
  },
};
</script>

<style lang="scss">
@import "./assets/style/common.scss";

body {
  background-color: rgb(94, 88, 88);
  background-image: url("../src/assets/img/netflix-image.jpg");
  background-blend-mode: multiply;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center top;
}
</style>