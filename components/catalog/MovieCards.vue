<template>
  <ul class="movie-cards">
    <li
      v-for="movie of movies"
      :key="movie.id"
      :class="{ 'movie-cards__item--active': isMovieActive(movie) }"
      class="movie-cards__item"
    >
      <MovieCard
        :movie="movie"
        :is-active="isMovieActive(movie)"
        :is-active-slideshow="isSlideshowActive(movie)"
        @activate="activateMovie($event)"
        @slideshow="activateSlideshow($event)"
        @close-details="closeDetails"
      />
    </li>
  </ul>
</template>

<script>
import MovieCard from './MovieCard'

export default {
  components: {
    MovieCard
  },
  props: {
    movies: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      activeMovie: null,
      activeSlideshow: null
    }
  },
  methods: {
    activateMovie (movie) {
      this.activeMovie = movie
      if (this.activeSlideshow !== movie) {
        this.activeSlideshow = null
      }
    },
    activateSlideshow (movie) {
      this.activeSlideshow = movie
    },
    isMovieActive (movie) {
      return this.activeMovie === movie
    },
    isSlideshowActive (movie) {
      return this.activeSlideshow === movie
    },
    closeDetails () {
      this.activeMovie = null
      this.activeSlideshow = null
    }
  }
}
</script>

<style lang="less">
@import "~@/assets/less/variables";

.movie-cards {
  display: flex;
  flex-wrap: wrap;
  margin: 0;
  padding: 9px 0;
  list-style: none;

  &__item {
    display: block;
    box-sizing: border-box;
    flex-basis: 25%;
    min-width: 258px; // 240px + 9px + 9px
    max-width: 338px; // 320px + 9px + 9px
    margin: 0 auto;
    padding: 9px;

    &--active {
      background: @bg-body;
    }

    // catching breakpoints where the cards begin to jump to next row
    @media (max-width: 1032px) {
      flex-basis: 33.33%;
    }

    @media (max-width: 773px) {
      flex-basis: 50%;
    }

    @media (max-width: 515px) {
      flex-basis: 100%;
    }
  }
}
</style>
