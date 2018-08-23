<template>
  <div class="optionsView">
    <label id="noteLabel" for="taskNote">Notes</label>
    <textarea
    id="taskNote"
    :value='notes'
    @change="updateNotes($event.target.value)"
    :disabled = '!editable'
    ></textarea>
    <label id="dueLabel" for="taskDueDate">Due Date</label>
    <input
    type="Date"
    id="taskDueDate"
    :value='dueDate'
    @change="updateDue($event.target.value)"
    :disabled = '!editable'
    :min="dueDate || new Date().toJSON().split('T')[0]"
    >
    <label id="priorLabel" for="taskPriority">Priority</label>
    <select
    id="taskPriority"
    :value='priority'
    @change="updatePrior($event.target.value)"
    :disabled = '!editable'
    >
      <option>Low</option>
      <option>Medium</option>
      <option>High</option>
    </select>
    <button
    id="saveButton"
    @click="updateAllOptions">Save</button>
  </div>
</template>

<script>
let newNote, newDue, newPrior
export default {
  name: 'Options',
  props: ['id', 'notes', 'dueDate', 'priority', 'editable'],
  methods: {
    updateNotes (newNoteValue) {
      newNote = newNoteValue
    },
    updateDue (newDueValue) {
      newDue = newDueValue
    },
    updatePrior (newPriorValue) {
      newPrior = newPriorValue
    },
    updateAllOptions () {
      let data = {
        'notes': newNote,
        'dueDate': newDue,
        'priority': newPrior
      }
      let myInit = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
      }

      fetch('http://localhost:3000/tasks/patch/' + this.id, myInit)
        .then(response => {
          this.$emit('update-options')
        })
    }
  }
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
  .optionsView #saveButton {
    grid-column: 2;
    grid-row: 5;
  }

</style>
