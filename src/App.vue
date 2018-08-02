<template>
  <div id="app">
    <open-tasks
    v-for="task in allTasks"
    :task="task"
    :key="allTasks.indexOf(task)"

    v-if="task.category === 'open'"
    @update-storage="updateStorage"
    />
    <div class="newTaskItem">
      <input type="text" placeholder="+    New Task" @keyup.enter="addTask">
    </div>
    <closed-tasks
    v-for="task in allTasks"
    :task="task"
    :key="allTasks.indexOf(task)"

    v-if="task.category === 'closed'"
    />

  </div>
</template>

<script>
import OpenTasks from './components/OpenTasks'
import ClosedTasks from './components/ClosedTasks'

var allTasks = []
if (localStorage.getItem('tasks') !== null) {
  allTasks = JSON.parse(localStorage.getItem('tasks'))
}

export default {
  name: 'App',
  data () {
    return {
      allTasks
    }
  },
  components: {
    'open-tasks': OpenTasks,
    'closed-tasks': ClosedTasks
  },
  methods: {
    addTask (event) {
      this.allTasks.push({'desc': event.target.value, 'category': 'open'})
      this.updateStorage()
      event.target.value = ''
    },
    updateStorage () {
      localStorage.setItem('tasks', JSON.stringify(allTasks))
    }
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
