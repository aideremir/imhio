<template>
  <div v-if="tags.length" class="movie-tags">
    <b v-if="label">{{ label }}:</b>&nbsp;
    <div
      v-for="(tag, index) of tags"
      :key="index"
      :style="{ background: color }"
      class="movie-tags__tag"
    >
      {{ tag }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    tags: {
      type: Array,
      default: () => []
    },
    color: {
      type: String,
      default: '#646464'
    }
  }
}
</script>

<style lang="less">
.movie-tags {
  margin-bottom: 9px;
  &__tag {
    display: inline-block;
    margin: 0 8px 8px 0;
    padding: 4px;
    border-radius: 4px;
    font-size: 14px;
    line-height: 16px;
    text-transform: capitalize;
  }
}
</style>
