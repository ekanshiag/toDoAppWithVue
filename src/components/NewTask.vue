<template>
  <input
    type="text"
    placeholder="+    New Task"
    v-on="listeners"
  >
</template>

<script>
export default {
  name: 'NewTask',
  computed: {
    listeners () {
      return {
        ...this.$listeners,
        input: event => this.$emit('input', event.target.value)
      }
    }
  }
}
</script>
