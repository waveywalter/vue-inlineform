<template>
  <div id="app">
      <FormBuilder></FormBuilder>
  </div>
</template>

<script>

import FormBuilder from './components/FormBuilder.vue'
export default {
  name: 'app',
  components: {
   FormBuilder
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
