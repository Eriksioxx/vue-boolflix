<template>
  <main>
    <!-- TRADING -->
    <h3 v-if="this.trendingMovies.length != 0 && this.movie.length === 0"></h3>

    <div v-if="this.movie.length === 0">
      <FlixTrend :trendingMovies="trendingMovies" :trendingTv="trendingTv" />
    </div>

    <!-- FINE TRADING -->

    <div v-else>
      <FlixMovies :infoMovie="movie" />
      <FlixSeries :infoSeries="series" />
    </div>
  </main>
</template>

<script>
import FlixMovies from "./partials/FlixMovies.vue";
import FlixSeries from "./partials/FlixSeries.vue";
import FlixTrend from "./partials/FlixTrend.vue";

export default {
  name: "FlixMain",

  props: {
    movie: Array,
    series: Array,
    trendingMovies: Array,
    trendingTv: Array,
  },

  components: {
    FlixMovies,
    FlixSeries,
    FlixTrend,
  },

  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped lang="scss">
@import "../assets/style/common.scss";

main {
  // background-color: gray;

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  ul.gallery {
    display: flex;
    flex-wrap: wrap;
  }

  .card {
    padding: 10px;
    border: 1px solid black;
    width: calc(100% / 4);
    text-align: center;

    img {
      width: 100%;
      object-fit: contain;
    }
  }
}
</style>
