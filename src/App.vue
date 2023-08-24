<template>
  <div class="container">
    <Cards />
  </div>
</template>

<script setup>
import Cards from './components/Cards.vue';
</script>

<style lang="scss">
  #app {
    padding: 40px;
    width: 100%;
    @include tablet {
      padding: 0 40px;
    }
  }
  .container {
    margin: auto auto;
    display: flex;
    max-width: 500px;
    @include tablet {
      overflow: visible;
      align-items: center;
      max-width: 615px;
    }
    @include desktop {
      max-width: 1000px;
    }
  }
</style>
