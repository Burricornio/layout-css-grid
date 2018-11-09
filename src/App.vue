<template lang="pug">
  div(id="app")
    layout
</template>

<script>
import Layout from './components/Layout.vue'

export default {
  name: 'app',
  components: {
    Layout
  }
}
</script>

<style lang="scss">
@import './scss/main.scss';

  body {
    margin: 0;
    padding: 0;
    font-family: $main-font-family;
    font-size: 1.125rem;
    font-weight: 700;
    color: $main-font-color;
    overflow: hidden;

    * {
      box-sizing: border-box;
    }
  }
</style>
