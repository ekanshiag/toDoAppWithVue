<template>
  <div>
    <label for="taskNote">Notes</label>
    <textarea id="taskNote" v-model='notes'></textarea>
    <label for="taskDueDate">Due Date</label>
    <input type="Date" id="taskDueDate" :value='dueDate'>
    <label for="taskPriority">Priority</label>
    <select id="taskPriority" :value='priority'>
      <option>Low</option>
      <option>Medium</option>
      <option>High</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'Options',
  props: ['notes', 'dueDate', 'priority']
}
</script>
