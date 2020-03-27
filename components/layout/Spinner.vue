<template>
  <div class="spinner" />
</template>

<style lang="less">
@keyframes spinner-rotate {
  0% {
    transform: rotate(0);
  }
  100% {
    transform: rotate(360deg);
  }
}

.spinner {
  border-radius: 50%;
  animation-name: spinner-rotate;
  animation-duration: 0.6s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  border-style: solid;
  width: 22px;
  height: 22px;
  border-width: 2px;
  transform-origin: 50% 50% calc((22px / 2) + 2px);
  border-color: rgba(255, 255, 255, 0.8);
  border-top-color: #808080;
}
</style>
