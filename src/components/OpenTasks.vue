<template>
  <div>
    {{task.desc}}
  </div>
</template>

<script>
export default{
  name: 'OpenTasks',
  props: {
    task: Object
  }
}
</script>
