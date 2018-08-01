<template>
  <div>
  <input type="checkbox" value="task.desc">
  <p>{{task.desc}}</p>
  <Options/>
  </div>
</template>

<script>
export default{
  name: 'OpenTasks',
  props: ['task']
}
</script>
