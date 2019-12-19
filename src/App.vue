<template>
  <div id="app">
    <BirdsEye :props="{}" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import BirdsEye from './components/BirdsEye.vue';

export default Vue.extend({
  name: 'app',
  components: {
    BirdsEye,
  },
  async mounted() {
    await import('./components/BirdsEye.vue');
  },
});
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
