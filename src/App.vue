<template>
  <div id="app">
    <MainScreen/>
  </div>
</template>

<script>
import MainScreen from './components/MainScreen'

export default {
  name: 'App',
  components: {
    MainScreen
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  width: 100%;
  height: 100vh;
}
body {
  background-color: #D7D7D7;
  font-family: 'Open Sans';
}
</style>
