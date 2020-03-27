<template>
  <div class="movies-header">
    <h1 class="movies-header__title">
      Best <span>{{ tag }}</span> porn movies
    </h1>
    <div class="movies-header__total">
      Total videos: {{ total }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tag: {
      type: String,
      default: ''
    },
    total: {
      type: Number,
      default: 0
    }
  }
}
</script>

<style lang="less">
@import "~@/assets/less/variables";

.movies-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 9px;
  background: @bg-body;

  &__title {
    margin: 0;
    font-weight: normal;
    font-size: 20px;
    line-height: 23px;

    span {
      text-transform: uppercase;
    }
  }

  &__total {
    font-size: 14px;
    line-height: 16px;

    // considering 576px is the breakpoint for phones
    @media (max-width: 576px) {
      display: none;
    }
  }
}
</style>
