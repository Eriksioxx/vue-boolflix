<template>
  <li class="card">
    <div class="flip-card">
      <!-- Inizio flip card inner -->
      <div class="flip-card-inner">
        <!-- Inizio front -->
        <div class="flip-card-front">
          <img
            :src="'https://image.tmdb.org/t/p/w342/' + product.poster_path"
          />
        </div>
        <!-- Fine front -->
        <!-- Inizio back -->
        <div class="flip-card-back">
          <div class="card-details">
            <h1>{{ product.title ? product.title : product.name }}</h1>
            <h2>
              {{
                product.original_title
                  ? product.original_title
                  : product.original_name
              }}
            </h2>
            <lang-flag :iso="product.original_language" :squared="false" />
            <h4>Voto: {{ product.vote_average }}</h4>

            <p>{{ product.overview }}</p>
          </div>

          <div class="rating" v-for="(n, index) in 5" :key="index">
            <font-awesome-icon
              :class="
                n <= Math.ceil(product.vote_average / 2) ? 'star-red' : ''
              "
              :icon="
                Math.ceil(product.vote_average / 2) == 0
                  ? 'fa-solid fa-ban'
                  : 'fa-solid fa-star'
              "
            />
          </div>
        </div>
        <!-- Fine back -->
      </div>
      <!-- Fine flip card inner -->
    </div>
  </li>
</template>

<script>
export default {
  name: "FlixCard",
  props: {
    product: Object,
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

    // Inizio card
    .card {
      width: calc(100% / 4 - 20px);
      text-align: center;
      margin: 10px;
      background-color: transparent;

      &:hover .flip-card-inner {
        transform: rotateY(180deg) scale(1.2) translateZ(200px);
      }

      img {
        width: 100%;
        object-fit: contain;
        display: block;
      }

      // Inizio rating
      .rating {
        display: inline-block;

        .star-red {
          color: red;
        }
      }
      // Fine rating

      // Inizio flip card
      .flip-card {
        background-color: transparent;
        perspective: 1000px;
        width: 100%;
        height: 100%;

        // Inizio flip card inner
        .flip-card-inner {
          position: relative;
          width: 100%;
          height: 100%;
          text-align: center;
          transition: transform 0.7s;
          transform-style: preserve-3d;

          // Inizio flip card front e back
          .flip-card-front,
          .flip-card-back {
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            background-color: rgba($color: #000000, $alpha: 0.5);
            color: white;
          }

          .flip-card-back {
            position: absolute;
            top: 0;
            right: 0;
            transform: rotateY(180deg);
            overflow-y: auto;

            .card-details * {
              padding: 5px;
            }
          }
          // Fine flip card front e back
        }
        // Fine flip card inner
      }
      // Fine flip card
    }
    // Fine card
  }
  // Fine ul
}
// Fine container
</style>