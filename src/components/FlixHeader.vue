<template>
  <header>
    <h1 id="site-name">BOOLFLIX</h1>

    <select
      v-model="targetGenre"
      @change="$emit('SelectionGenre', targetGenre)"
    >
      <option value selected="Tutti i generi">Tutti i generi</option>
      <option v-for="(product, index) in genre" :key="index" :value="option">
        {{ product.name }}
      </option>
    </select>

    <form class="searchPanel">
      <input
        type="text"
        placeholder="Cerca il tuo film o la tua serie TV preferita"
        v-model="inputSearch"
      />
      <button type="submit" @click.prevent="$emit('search', inputSearch)">
        Cerca
      </button>
    </form>
  </header>
</template>

<script>
export default {
  name: "FlixHeader",

  props: {
    genre: Array,
  },

  data() {
    return {
      inputSearch: "",
      targetGenre: "",
    };
  },
};
</script>

<style scoped lang="scss">
@import "../assets/style/common.scss";
header {
  height: 80px;
  // background-color: black;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 10px;

  input {
    width: 330px;
  }

  input,
  button {
    padding: 5px;
    font-size: 15px;
    text-align: center;

    margin-left: 5px;
  }
}
</style>
