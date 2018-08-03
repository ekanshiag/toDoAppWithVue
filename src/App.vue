<template>
  <div id="app">
    <h1>My tasks</h1>
    <open-tasks
    v-for="task in allTasks"
    :task="task"
    :key="allTasks.indexOf(task)"

    v-if="task.category === 'open'"
    @update-storage="updateStorage"
    @delete-task="deleteTask"
    />
    <div class="newTaskItem">
      <input type="text" placeholder="+    New Task" @keyup.enter="addTask">
    </div>
    <h1>Done</h1>
    <closed-tasks
    v-for="task in allTasks"
    :task="task"
    :key="allTasks.indexOf(task)"

    v-if="task.category === 'closed'"
    @delete-task="deleteTask"
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
      let newTask = event.target.value.trim()
      if (!/\w+/.test(newTask)) {
        alert('Invalid task')
        return
      }
      this.allTasks.unshift({'desc': newTask, 'category': 'open'})
      this.updateStorage()
      event.target.value = ''
    },
    updateStorage () {
      localStorage.setItem('tasks', JSON.stringify(this.allTasks))
    },
    deleteTask (taskToRemove) {
      this.allTasks = this.allTasks.filter(x => { return x !== taskToRemove })
      this.updateStorage()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
  background-color:  #eff2f6
}
</style>
