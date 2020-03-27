<template>
  <div class="main-page">
    <MoviesHeader v-if="info" :tag="info.search_term" :total="info.total" />
    <MovieCards :movies="movies" />
    <div v-show="isDataLoading" class="main-page__load-more">
      <Spinner />
    </div>
  </div>
</template>

<script>
import MoviesHeader from '~/components/catalog/MoviesHeader'
import Spinner from '~/components/layout/Spinner'
import MovieCards from '~/components/catalog/MovieCards'

const MOVIES_LIMIT = 12

export default {
  components: {
    MoviesHeader,
    Spinner,
    MovieCards
  },
  data () {
    return {
      isDataLoading: false,
      info: null,
      movies: [],
      allMovies: [],
      offset: 0
    }
  },
  computed: {
    canLoadMore () {
      return this.movies.length < this.allMovies.length || this.offset === 0
    }
  },
  mounted () {
    this.getAll()
    this.getPage()
    window.addEventListener('scroll', this.watchScroll)
  },
  destroyed () {
    window.removeEventListener('scroll', this.watchScroll)
  },
  methods: {
    // Imitating per-page loading by fetching all data and then loading slices on scroll
    async getAll () {
      const response = await fetch('/result.json')
      if (!response.ok) {
        alert('Error loading data!')
        this.isDataLoading = false
        return
      }
      const data = await response.json()
      this.allMovies = data.item
      this.info = data.info
    },
    getPage () {
      if (!this.canLoadMore) {
        return
      }
      this.isDataLoading = true

      // adding setTimeout to imitate long data loading
      setTimeout(() => {
        // slicing full array and appending slice to result to imitate per-page loading
        this.movies = this.movies.concat(
          this.allMovies.slice(this.offset, this.offset + MOVIES_LIMIT)
        )

        this.isDataLoading = false
        this.offset += MOVIES_LIMIT
      }, 1000)
    },
    watchScroll () {
      const d = document.documentElement
      const offset = d.scrollTop + window.innerHeight
      const height = d.offsetHeight

      if (offset >= height) {
        this.getPage()
      }
    }
  }
}
</script>

<style lang="less">
  .main-page {
    &__load-more {
      display: flex;
      justify-content: center;
      margin-bottom: 9px;
    }
  }
</style>
