<template>
  <div class="done">
    <input type="checkbox" id="taskItem" :value='task.desc' @click="updateTaskCategory" checked>
    <label id="taskDesc" for="taskItem">{{task.desc}}</label>
    <button id="delete" @click="deleteTask">X</button>
    <button @click='showOptions = !showOptions'>^</button>
    <options
    :notes='task.notes'
    :dueDate='task.dueDate'
    :priority='task.priority'
    :editable='false'
    v-if="showOptions"
    />
  </div>
</template>

<script>
import Options from './Options.vue'
export default{
  name: 'ClosedTasks',
  data () {
    return {
      showOptions: false
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
        'category': 'Open'
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
    deleteTask () {
      let myInit = {
        method: 'POST'
      }
      fetch('http://localhost:3000/tasks/delete/' + this.task.id, myInit)
        .then(response => {
          this.$emit('update-tasks')
        })
    }
  }
}
</script>

<style>
  .done #taskDesc {
    text-decoration: line-through;
  }
  .done > input, .done > label {
    padding: 15px;
  }
  .done button {
    padding: 0;
    float: right;
  }
  .done #delete {
    color: red;
  }
</style>
