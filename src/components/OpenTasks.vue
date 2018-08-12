<template>
  <div class="taskItem">
    <input type="checkbox" :value='task.desc' @click="updateTaskCategory">
    <label @dblclick="editTask = true" v-if="!editTask">{{task.desc}}</label>
    <input type="text" v-model="task.desc" v-if="editTask" @change="editTask=false">
    <button @click='showOptions = showOptions ? false : true'>^</button>
    <button id="delete" @click="deleteTask">X</button>
    <options
    :notes='task.notes'
    :dueDate='task.dueDate'
    :priority='task.priority'
    :editable='true'
    v-if="showOptions"

    @update-notes="updateNotes"
    @update-due="updateDue"
    @update-priority="updatePriority"
    />
  </div>
</template>

<script>
import Options from './Options.vue'

export default{
  name: 'OpenTasks',
  data () {
    return {
      showOptions: false,
      editTask: false
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
      this.task.category = 'closed'
      this.$emit('update-storage')
    },
    updateNotes (newNotes) {
      this.task.notes = newNotes
      this.$emit('update-storage')
    },
    updateDue (newDue) {
      this.task.dueDate = newDue
      this.$emit('update-storage')
    },
    updatePriority (newPrior) {
      this.task.priority = newPrior
      this.$emit('update-storage')
    },
    deleteTask () {
      this.$emit('delete-task', this.task)
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
</style>
