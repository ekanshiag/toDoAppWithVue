<template>
  <div>
  <h1>Tasks to do</h1>
  <OpenTasks
    v-for="task in allTasks"
    :key="task.id"
    :task="task"

    v-if="task.category === 'open'"
  />
  <NewTask
    v-model="newToDo"
    @keydown.enter = "addTask"
    />
  <h1>Done</h1>
  <ClosedTasks
    v-for="task in allTasks"
    :key="task.id"
    :task="task"

    v-if="task.category === 'closed'"
  />
  </div>
</template>

<script>
import OpenTasks from './OpenTasks'
import NewTask from './NewTask'
import ClosedTasks from './ClosedTasks'

let taskList = []

export default{
  name: 'TaskLists',
  components: {
    OpenTasks,
    NewTask,
    ClosedTasks
  },
  data () {
    if (localStorage.getItem('tasks') !== null) {
      taskList = JSON.parse(localStorage.getItem('tasks'))
    }
    return {
      newToDo: '',
      allTasks: taskList
    }
  },
  methods: {
    addTask () {
      this.allTasks.push({
        'desc': this.newToDo,
        'category': 'open',
        'notes': '',
        'dueDate': '',
        'priority': ''
      })
      this.newToDo = ''
    }
  }
}

</script>
