<template>
  <div>
    <input type="checkbox" id="taskItem" :value='task.desc' @click="task.category = 'open'">
    <label for="taskItem">{{task.desc}}</label>
    <a @click='showOptions = showOptions ? false : true'>^</a>
    <options
    :notes='task.notes'
    :dueDate='task.dueDate'
    :priority='task.priority'
    v-if="showOptions"
    />
    <button @click="deleteTask">Delete</button>
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
    deleteTask () {
      this.$emit('delete-task', this.task)
    }
  }
}
</script>
