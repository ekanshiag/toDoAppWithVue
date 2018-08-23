<template>
  <div id="app">
    <h1>My tasks</h1>
    <open-tasks
    class = 'myTasks'
    v-for="task in allTasks"
    :task="task"
    :key="allTasks.indexOf(task)"

    v-if="task.category === 'Open'"
    @update-tasks="updateTasks"
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

    v-if="task.category === 'Closed'"
    @update-tasks="updateTasks"
    />
  </div>
</template>

<script>
import OpenTasks from './components/OpenTasks'
import ClosedTasks from './components/ClosedTasks'

let allTasks = []

export default {
  name: 'App',
  data () {
    fetch('http://localhost:3000/tasks/')
      .then(response => {
        return response.json()
      })
      .then(tasks => {
        console.log(tasks)
        this.allTasks = tasks
      })
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

      let data = {
        'category': 'Open',
        'desc': newTask,
        'notes': '',
        'dueDate': '',
        'priority': ''
      }

      let myInit = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
      }

      fetch('http://localhost:3000/tasks/', myInit)
        .then(response => {
          event.target.value = ''
          this.updateTasks()
        })
    },
    updateTasks () {
      fetch('http://localhost:3000/tasks/')
        .then(response => {
          return response.json()
        })
        .then(tasks => {
          this.allTasks = tasks
        })
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
