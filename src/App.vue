<template>
  <div id="app">
    <Main />
  </div>
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style>
#app {
  min-width: 100vw;  
  min-height: 100vh;
}

* {
  padding: 0;
  margin: 0;
}
</style>
