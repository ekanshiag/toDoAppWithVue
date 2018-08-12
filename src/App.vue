<template>
  <div id="app">
    <h1>My tasks</h1>
    <open-tasks
    class = 'myTasks'
    v-for="task in allTasks"
    :task="task"
    :key="allTasks.indexOf(task)"

    v-if="task.category === 'open'"
    @update-storage="updateStorage"
    @delete-task="deleteTask"
    />
    <div class="newTaskItem">
      <input type="text" placeholder="+    New Task" @keyup.enter="addTask" id="newTask">
    </div>
    <h1>Done</h1>
    <closed-tasks
    class = 'completedTasks'
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
  background-color:  #eff2f6;
}

#app h1 {
  text-align: center;
  padding-top: 1em;
}

#newTask {
  margin-top: 2em;
  width: 98%;
  height: 2em;
  color: #ffffff;
  background-color: #5c7ba3;
  border: 3px solid #ced7e3;
  border-radius: 1em;
}

.myTasks, .completedTasks {
  border: 3px solid #adbdd1;
  border-radius: 1em;
  background-color: #dee5ed;
  box-sizing: content-box;
  margin: 0.5em;
  padding: 1em;
}
</style>
