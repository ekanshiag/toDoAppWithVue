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
  }
}
</script>
