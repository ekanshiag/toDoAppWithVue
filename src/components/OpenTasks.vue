<template>
  <div class="taskItem">
    <input type="checkbox" :value='task.desc' @click="updateTaskCategory">
    <label @dblclick="editTask = true" v-if="!editTask">{{task.desc}}</label>
    <input type="text" :value="task.desc" v-if="editTask" @change="updateTaskDesc($event.target.value)">
    <button id="delete" @click="deleteTask">X</button>
    <button @click='showOptions = !showOptions'>^</button>
    <options
    :id='task.id'
    :notes='task.notes'
    :dueDate='task.dueDate'
    :priority='task.priority'
    :editable='true'
    v-if="showOptions"

    @update-options="updateOptions"
    />
    <label
    id="dueDate"
    v-else
    >{{date}}</label>
  </div>
</template>

<script>
import Options from './Options.vue'
import moment from 'moment'

export default{
  name: 'OpenTasks',
  data () {
    return {
      showOptions: false,
      editTask: false
    }
  },
  computed: {
    date: function () {
      let date = moment(this.task.dueDate).format('dddd, MMMM Do YYYY')
      return date !== 'Invalid date' ? date : ''
    }
  },
  props: {
    task: Object
  },
  components: {
    'options': Options
  },
  methods: {
    updateTaskCategory () {
      let data = {
        'category': 'Closed'
      }

      let myInit = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
      }

      fetch('http://localhost:3000/tasks/patch/' + this.task.id, myInit)
        .then(response => {
          this.$emit('update-tasks')
        })
    },
    updateTaskDesc (newTask) {
      let data = {
        'desc': newTask
      }
      let myInit = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
      }

      fetch('http://localhost:3000/tasks/patch/' + this.task.id, myInit)
        .then(response => {
          this.editTask = false
          this.$emit('update-tasks')
        })
    },
    deleteTask () {
      let myInit = {
        method: 'POST'
      }

      fetch('http://localhost:3000/tasks/delete/' + this.task.id, myInit)
        .then(response => {
          this.$emit('update-tasks')
        })
    },
    updateOptions () {
      this.$emit('update-tasks')
    }
  }
}
</script>

<style>
  .taskItem > input, .taskItem > label {
    padding: 15px;
  }
  .taskItem button {
    padding: 0;
    float: right;
  }
  .taskItem #delete {
    color: red;
  }
  .taskItem #dueDate {
    color: grey;
    float: right;
  }
</style>
