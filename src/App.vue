<template>
  <div id="app">
    <Contenido />
  </div>
</template>

<script>
import Contenido  from './components/Contenido'

export default {
  name: 'App',
  components: {
    Contenido
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
