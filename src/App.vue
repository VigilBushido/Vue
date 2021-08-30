<template>
  <div id="app">
    <!-- <Exercise /> -->
    <!-- <ShoppingCart /> -->
    <!-- <Exercise2 /> -->
    <ApiBlog />
  </div>
</template>

<script>
//import Exercise from './components/Exercise1-01'
//import Exercise2 from './components/Exercise2-01'
import ApiBlog from './components/ApiBlog.vue'
//import ShoppingCart from './components/ShoppingCart'

export default {
  name: 'app',
  components: {
    //Exercise2,
    ApiBlog, //ShoppingCart, //Exercise,
  },
}
</script>

<style lang="scss">
@import './styles/global';
</style>
