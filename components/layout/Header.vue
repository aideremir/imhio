<template>
  <header class="header">
    <nuxt-link to="/" class="header__logo">OZEEX</nuxt-link>
  </header>
</template>

<script>
export default {}
</script>

<style lang="less">
.header {
  padding: 9px;

  &__logo {
    font-size: 54px;
    line-height: 63px;
    color: #ffffff;
    text-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
    text-decoration: none;
  }
}
</style>
