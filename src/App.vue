<template>
  <div id="app">
    <div class="container">
      <Todos />
    </div>
    <!-- <Exercise /> component -->
  </div>
</template>

<script>
import Todos from './components/Todos.vue'
//import Exercise from './components/Exercise1-01'  //Exercise,

export default {
  name: 'app',
  components: {
    Todos,
  },
}
</script>

<style lang="scss">
@import './styles/global';
</style>
