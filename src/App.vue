<template>
  <div id="app">
    <TaskLists/>
  </div>
</template>

<script>
import TaskLists from './components/TaskLists.vue'

export default {
  name: 'App',
  components: {
    TaskLists
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
