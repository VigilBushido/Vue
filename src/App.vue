<template>
  <div id="app">
    <div class="container">
      <Exercise />
    </div>
  </div>
</template>

<script>
import Exercise from './components/Exercise1-01'

export default {
  name: 'app',
  components: {
    Exercise,
  },
}
</script>

<style lang="scss">
@import './styles/global';
</style>
