<template>
  <div class="optionsView">
    <label id="noteLabel" for="taskNote">Notes</label>
    <textarea
    id="taskNote"
    v-model='notes'
    @change="$emit('update-notes', $event.target.value)"
    :disabled = '!editable'
    ></textarea>
    <label id="dueLabel" for="taskDueDate">Due Date</label>
    <input
    type="Date"
    id="taskDueDate"
    :value='dueDate'
    @change="$emit('update-due', $event.target.value)"
    :disabled = '!editable'
    >
    <label id="priorLabel" for="taskPriority">Priority</label>
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

<style>
  .optionsView {
    display: grid;
    grid-template-columns:2fr 1fr;
    column-gap: 10px;
  }
  .optionsView #noteLabel {
    grid-column:1;
    grid-row:1;
  }
  .optionsView #taskNote {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    grid-column:1;
    grid-row: 2/5;
  }
  .optionsView #dueLabel {
    grid-column:2;
    grid-row:1;
  }
  .optionsView #taskdueDate {
    grid-column:2;
    grid-row: 2;
  }
  .optionsView #priorLabel {
    grid-column:2;
    grid-row: 3;
  }
  .optionsView #taskPriority {
    grid-column:2;
    grid-row: 4;
  }

</style>
