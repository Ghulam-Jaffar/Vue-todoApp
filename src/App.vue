<template>
  <div id="app">
    <TodoApp :nbr="nbr" msg="v1.1"></TodoApp>
  </div>
</template>

<script>

import TodoApp from './components/TodoApp.vue'

export default {
  name: 'App',
  data(){
    return{
       nbr:22,
    }
  },
  components: {
    TodoApp,
}
}
</script>

<style>

</style>
