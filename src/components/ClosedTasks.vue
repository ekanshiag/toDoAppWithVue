<template>
  <div>
    {{task.desc}}
  </div>
</template>

<script>
export default{
  name: 'ClosedTasks',
  props: {
    task: Object
  }
}
</script>
