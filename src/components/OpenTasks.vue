<template>
  <div>
    <input type="checkbox" :value='task.desc' @click="task.category = 'closed'">
    <label @dblclick="editTask = true" v-if="!editTask">{{task.desc}}</label>
    <input type="text" v-model="task.desc" v-if="editTask" @change="editTask=false">
    <a @click='showOptions = showOptions ? false : true'>^</a>
    <options
    :notes='task.notes'
    :dueDate='task.dueDate'
    :priority='task.priority'
    v-if="showOptions"

    @update-notes="updateNotes"
    @update-due="updateDue"
    @update-priority="updatePriority"
    />
    <button>Delete</button>
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
    }
  }
}
</script>
