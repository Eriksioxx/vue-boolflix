<template>
  <section>
    <h1 class="main-title">FILM</h1>
    <div class="container">
      <ul class="gallery">
        <FlixCard
          v-for="(product, i) in trendingMovies"
          :key="i"
          :product="product"
          type="movie"
        />
        <FlixCard
          v-for="(product, index) in trendingTv"
          :key="index"
          :product="product"
          type="series"
        />
      </ul>
    </div>

    <h1 class="main-title">SERIE TV</h1>
    <div class="container">
      <ul class="gallery">
        <FlixCard
          v-for="(product, index) in trendingTv"
          :key="index"
          :product="product"
          type="series"
        />
      </ul>
    </div>
  </section>
</template>

<script>
import FlixCard from "./FlixCard.vue";

export default {
  name: "FlixTrend",
  props: {
    infoMovie: Array,
    trendingMovies: Array,
    trendingTv: Array,
  },
  components: {
    FlixCard,
  },
  data() {
    return {
      //   display: null,
    };
  },
  methods: {
    //     showDetails(index) {
    //       this.display = index;
    //       console.log(this.display);
    //     },
    //     showCover() {
    //       this.display = null;
    //       console.log(this.display);
    //     },
  },
};
</script>

<style scoped lang="scss">
@import "../../assets/style/common.scss";
// Inizio container
.container {
  max-width: 1200px;
  margin: 0 auto;

  // Inizio ul
  ul.gallery {
    display: flex;
    flex-wrap: wrap;
  }
  // Fine ul
}
// Fine container
</style>