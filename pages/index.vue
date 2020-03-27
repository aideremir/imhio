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
import AllMovies from '~/assets/data/result.js' // importing data instead of real backend server

import MoviesHeader from '~/components/catalog/MoviesHeader'
import Spinner from '~/components/layout/Spinner'
import MovieCards from '~/components/catalog/MovieCards'

const MOVIES_LIMIT = 12
const META_KEYWORDS_LIMIT = 20

export default {
  components: {
    MoviesHeader,
    Spinner,
    MovieCards
  },
  data () {
    return {
      isDataLoading: false,
      info: AllMovies.info,
      allMovies: AllMovies.item,
      movies: AllMovies.item.slice(0, MOVIES_LIMIT),
      offset: MOVIES_LIMIT
    }
  },
  computed: {
    canLoadMore () {
      return this.movies.length < this.allMovies.length || this.offset === 0
    },
    metaKeywords () {
      let tags = []
      for (let i = 0; i < MOVIES_LIMIT; i++) {
        tags = tags.concat(this.movies[i].tag)
      }
      return [...new Set(tags)].slice(0, META_KEYWORDS_LIMIT).join(',')
    }
  },
  mounted () {
    window.addEventListener('scroll', this.watchScroll)
  },
  destroyed () {
    window.removeEventListener('scroll', this.watchScroll)
  },
  methods: {
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
  },
  head () {
    return {
      title: `Best ${this.info.search_term} porn movies`,
      meta: [
        { name: 'description', content: `Best ${this.info.search_term} porn movies. ${this.metaKeywords}` },
        { name: 'keywords', content: this.metaKeywords }
      ]
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
