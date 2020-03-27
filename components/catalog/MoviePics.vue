<template>
  <div class="movie-pics" @click="toggleSlideshow">
    <img :src="currentPicturePath" :alt="movie.description">
  </div>
</template>

<script>
// TODO: Add images preloading
export default {
  props: {
    movie: {
      type: Object,
      default: () => ({})
    },
    isActive: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      index: 0,
      slideshowInterval: null
    }
  },
  computed: {
    currentPicturePath () {
      return this.movie.picture[this.index].path
    }
  },
  watch: {
    isActive (newVal) {
      if (newVal) {
        this.startSlideshow()
      } else {
        this.stopSlideshow()
      }
    }
  },
  methods: {
    toggleSlideshow () {
      if (this.slideshowInterval) {
        this.stopSlideshow()
      } else {
        this.$emit('click', this.movie)
      }
    },
    startSlideshow () {
      this.slideshowInterval = setInterval(() => {
        this.index++
        if (this.index === this.movie.picture.length) {
          this.index = 0
        }
      }, 1000)
    },
    stopSlideshow () {
      if (!this.slideshowInterval) {
        return
      }
      clearInterval(this.slideshowInterval)
      this.slideshowInterval = null
    }
  }
}
</script>

<style lang="less">
.movie-pics {
  cursor: pointer;
}
</style>
