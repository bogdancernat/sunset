<template>
  <div id="app">
    <Sunset />
  </div>
</template>

<script>
import Sunset from '@/components/Sunset.vue';

export default {
  name: 'app',
  components: {
    Sunset,
  },
};
</script>

<style lang="scss">
  $sky-color: #3e4b69;

  body {
    padding: 0;
    margin: 0;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    min-height: 100vh;
    background: $sky-color;
    overflow: hidden;
  }

  #app {
    min-height: 100vh;
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
