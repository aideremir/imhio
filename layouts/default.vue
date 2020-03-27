<template>
  <div class="container">
    <Header />
    <section class="container__body">
      <nuxt />
    </section>
    <Footer />
  </div>
</template>

<script>
import Header from '~/components/layout/Header.vue'
import Footer from '~/components/layout/Footer.vue'

export default {
  components: {
    Header,
    Footer
  }
}
</script>

<style lang="less">
@import "~@/assets/less/variables";

.container {
  position: relative;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  margin: 0 auto;
  max-width: 1340px;
  background: @bg-container;

  &__body {
    flex-grow: 1;
  }
}
</style>
