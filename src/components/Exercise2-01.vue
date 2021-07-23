<template>
  <section>
    <div class="container">
      <input v-model="firstName" placeholder="First name" />
      <input v-model="lastName" placeholder="Last name" />

      <h3 class="output">{{ fullName }}</h3>
    </div>
    <div class="container2">
      <input type="number" v-model="incrementOne" />
      <h3> Get input: {{ incrementOne }}</h3>

      <h5>Set division: {{ divideByTwo }}</h5>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      firstName: '',
      lastName: '',
      count: -1,
      divideByTwo: 0,
    }
  },
  computed: {
    fullName() {
      return `${this.firstName} ${this.lastName}`
    },
    incrementOne: {
      //getter
      get() {
        return this.count + 1
      },
      //setter
      set(val) {
        this.count = val - 1
        this.divideByTwo = val / 2
      },
    },
  },
}
</script>

<style></style>
