<template>
  <Button type="Button">^</Button>
  <OptionsDiv v-show="showOptions"/>
</template>

<script>
  import OptionsDiv from './components/OptionsDiv'
  
  let showOptions = false

  export default{
    name: 'Options',
    data(){

    }
  }