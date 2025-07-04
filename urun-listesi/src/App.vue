<template>
  <div id="app">
    <ProductList />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue'

export default {
  name: 'App',
  components: {
    ProductList
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #f5f5f5;
  min-height: 100vh;
  padding: 20px 0;
}

body {
  margin: 0;
  background-color: #f5f5f5;
}
</style>
