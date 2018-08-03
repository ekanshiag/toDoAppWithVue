<template>
  <div>
    <label for="taskNote">Notes</label>
    <textarea
    id="taskNote"
    v-model='notes'
    @change="$emit('update-notes', $event.target.value)"
    :disabled = '!editable'
    ></textarea>
    <label for="taskDueDate">Due Date</label>
    <input
    type="Date"
    id="taskDueDate"
    :value='dueDate'
    @change="$emit('update-due', $event.target.value)"
    :disabled = '!editable'
    >
    <label for="taskPriority">Priority</label>
    <select
    id="taskPriority"
    :value='priority'
    @change="$emit('update-priority', $event.target.value)"
    :disabled = '!editable'
    >
      <option>Low</option>
      <option>Medium</option>
      <option>High</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'Options',
  props: ['notes', 'dueDate', 'priority', 'editable']
}
</script>
