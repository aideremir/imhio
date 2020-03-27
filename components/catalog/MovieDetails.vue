<template>
  <div class="movie-details">
    <button class="movie-details__close" @click="close">
      &times;
    </button>
    <div class="movie-details__pics">
      <MoviePics
        :movie="movie"
        :is-active="isActiveSlideshow"
        @click="$emit('slideshow', $event)"
      />
    </div>
    <div class="movie-details__details">
      <div><b>Added:</b> {{ movie.added }}</div>
      <div><b>Duration:</b> {{ movie.duration }}</div>
      <div><b>Source:</b> {{ movie.source }}</div>
    </div>
    <div class="movie-details__description">
      <b>Description:</b> {{ descriptionCut }}
    </div>
    <MovieTags :tags="movie.tag" label="Tags" />
    <MovieTags :tags="movie.pornstar" label="Pornstars" color="#0959CF" />
    <MovieTags :tags="movie.webcam" label="Webcam Models" color="#32A567" />
  </div>
</template>

<script>
import MovieTags from './MovieTags'
import MoviePics from './MoviePics'

export default {
  components: {
    MovieTags,
    MoviePics
  },
  props: {
    movie: {
      type: Object,
      required: true
    },
    isActiveSlideshow: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    descriptionCut () {
      return this.movie.description.substring(0, 800)
    }
  },
  methods: {
    close () {
      this.$emit('close')
    }
  }
}
</script>

<style lang="less">
@import "~@/assets/less/variables";

.movie-details {
  position: absolute;
  left: 0;
  right: 0;
  padding: 9px;
  background: @bg-body;

  @media (max-width: 576px) {
    padding-top: 30px;
  }

  &__close {
    display: none;
    position: absolute;
    top: 0;
    right: 0;
    width: 30px;
    height: 30px;
    color: @text-color;
    background: transparent;
    border: none;
    font-size: 22px;
    cursor: pointer;

    @media (max-width: 576px) {
      display: block;
    }
  }

  &__pics {
    display: none;

    @media (max-width: 576px) {
      display: flex;
      justify-content: center;
      margin-bottom: 15px;
    }
  }

  // considering 576px is the breakpoint for phones
  @media (max-width: 576px) {
    position: fixed; // TODO: lock scroll on body
    top: 0;
    bottom: 0;
  }

  &__details {
    display: none;
    font-size: 14px;
    line-height: 16px;

    @media (max-width: 576px) {
      display: block;
    }

    & > div {
      margin-bottom: 14px;
    }
  }

  &__description {
    margin-bottom: 9px;
  }
}
</style>
