<template>
  <section>
    <h1 class="main-title">FILM</h1>
    <div class="container">
      <ul class="gallery"></ul>
    </div>
  </section>
</template>

<script>
export default {
  name: "FlixMovies",
  props: {
    infoMovie: Array,
    infoGenre: Array,
  },
  data() {
    return {};
  },
};
</script>

<style scoped lang="scss">
</style>