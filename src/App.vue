<template>
  <div id="app">
    <calculator>
    </calculator>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body {
  background: rgb(123, 196, 185);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
