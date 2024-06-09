<script>
import MainTimer from './components/MainTimer.vue'

export default {
  name: 'App',
  components: {
    MainTimer
  }
}
</script>

<template>
  <div id="app">
    <MainTimer />
  </div>
</template>

<style scoped>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f5f5f5;
}
</style>
