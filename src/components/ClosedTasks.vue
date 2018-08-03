<template>
  <div class="done">
    <input type="checkbox" id="taskItem" :value='task.desc' @click="updateTaskCategory" checked>
    <label id="taskDesc" for="taskItem">{{task.desc}}</label>
    <a @click='showOptions = showOptions ? false : true'>^</a>
    <options
    :notes='task.notes'
    :dueDate='task.dueDate'
    :priority='task.priority'
    :editable='false'
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
    updateTaskCategory () {
      this.task.category = 'open'
      this.$emit('update-storage')
    },
    deleteTask () {
      this.$emit('delete-task', this.task)
    }
  }
}
</script>

<style>
  .done #taskDesc {
    text-decoration: line-through;
  }
</style>
