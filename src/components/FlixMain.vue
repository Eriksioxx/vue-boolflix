<template>
  <main>
    <FlixMovies :infoMovie="movie" :infoGenre="genre" />
    <FlixSeries :infoSeries="series" />
  </main>
</template>

<script>
import FlixMovies from "./partials/FlixMovies.vue";
import FlixSeries from "./partials/FlixSeries.vue";

export default {
  name: "FlixMain",

  props: {
    movie: Array,
    series: Array,
    genre: Array,
  },

  components: {
    FlixMovies,
    FlixSeries,
  },

  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped lang="scss">
@import "../assets/style/common.scss";
</style>
