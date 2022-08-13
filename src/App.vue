<template>
  <Home />
</template>

<script>
import Home from './views/Home.vue';

export default {
  name: 'App',
  components: { Home },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 1000px;
  margin: 0 auto;
  padding: 0;
}
</style>
