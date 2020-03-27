<template>
  <div
    class="movie-card"
    :class="{ 'movie-card--active': isActive }"
    :style="{ marginBottom: `${extraHeight}px` }"
  >
    <div class="movie-card__image">
      <MoviePics
        :movie="movie"
        :is-active="isActiveSlideshow"
        @click="$emit('slideshow', $event)"
      />
    </div>
    <template v-if="isActive">
      <div class="movie-card__details">
        <div><b>Added:</b> {{ movie.added }}</div>
        <div><b>Duration:</b> {{ movie.duration }}</div>
        <div><b>Source:</b> {{ movie.source }}</div>
      </div>
      <MovieDetails
        ref="details"
        :movie="movie"
        :is-active-slideshow="isActiveSlideshow"
        @slideshow="$emit('slideshow', $event)"
        @close="$emit('close-details')"
      />
    </template>
    <template v-else>
      <div class="movie-card__params">
        <div>Added: {{ movie.added }}</div>
        <div>Duration: {{ movie.duration }}</div>
      </div>
      <div class="movie-card__description">
        {{ movie.description }}
      </div>
      <div class="movie-card__tags">
        <MovieTags :tags="movie.tag" />
      </div>
      <button class="movie-card__button" @click="showInfo">
        More info
      </button>
    </template>
  </div>
</template>

<script>
import MovieTags from './MovieTags'
import MovieDetails from './MovieDetails'
import MoviePics from './MoviePics'

export default {
  components: {
    MovieTags,
    MovieDetails,
    MoviePics
  },
  props: {
    movie: {
      type: Object,
      required: true
    },
    isActive: {
      type: Boolean,
      default: false
    },
    isActiveSlideshow: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      extraHeight: 0
    }
  },
  watch: {
    isActive (newVal) {
      if (newVal) {
        this.$nextTick(() => {
          this.extraHeight = this.$refs.details.$el.offsetHeight + 5
        })
      } else {
        this.extraHeight = 0
      }
    }
  },
  methods: {
    showInfo () {
      this.$emit('activate', this.movie)
    }
  }
}
</script>

<style lang="less">
@import "~@/assets/less/variables";

.movie-card {
  &__image {
    margin-bottom: 5px;

    img {
      display: block;
      width: 100%;
    }
  }
  &__details {
    font-size: 14px;
    line-height: 16px;
    padding-top: 20px;

    & > div {
      margin-bottom: 14px;
    }
  }
  &__params {
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
    font-size: 10px;
    line-height: 12px;
  }

  &__description {
    margin-bottom: 10px;
    font-size: 14px;
    line-height: 16px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  &__tags {
    height: 24px; // two paddings + line height
    overflow: hidden;
    margin-bottom: 8px;

    // considering 576px is the breakpoint for phones
    @media (max-width: 576px) {
      display: none;
    }
  }

  &__button {
    width: 100%;
    cursor: pointer;
    padding: 6px 0;
    background: @bg-accent-2;
    border-radius: 3px;
    color: @text-color;
    border: none;

    &:hover {
      background: @bg-body;
    }
  }
}
</style>
