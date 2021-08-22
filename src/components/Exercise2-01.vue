<template>
  <section>
    <div class="container">
      <input v-model="firstName" placeholder="First name" />
      <input v-model="lastName" placeholder="Last name" />

      <h3 class="output">{{ fullName }}</h3>
    </div>
    <div class="container">
      <input type="number" v-model="incrementOne" />
      <h3> Get input: {{ incrementOne }}</h3>

      <h5>Set division: {{ divideByTwo }}</h5>
    </div>
    <div class="container">
      <h1>Shop Watcher</h1>
      <div>
        Black Friday Sale
        <strike> was {{ oldDiscount }}%</strike>
        <strong> Now {{ discount }}% OFF</strong>
      </div>
    </div>
    <br />
    <a href="#" @click="updateDiscount">Increase Discount!</a>
    <div class="container">
      <h1>Organization Watcher</h1>
      <div>
        Change of Name
        <strong> : {{ organization.name }}</strong>
        <strong> : {{ organization.employees }}</strong>
      </div>
    </div>
    <br />
    <a href="#" @click="changeName">Add Optimized!</a>
    <div class="container">
      <h1>Methods vs watchers vs computed props</h1>

      <div class="col">
        <input
          type="text"
          placeholder="Search with methd"
          v-model="input"
          @keyup="searchMethod"
        />

        <ul>
          <li v-for="(item, i) in methodFilterList" :key="i"> {{ item }} </li>
        </ul>
      </div>
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
      oldDiscount: 0,
      discount: 5,
      //object from which we watch keys for changes
      organization: {
        name: 'None',
        employees: ['Sergio', 'John', 'Omar', 'Maria', 'Tasha'],
      },
      frameworkList: [
        'Vue',
        'React',
        'Backbone',
        'Ember',
        'Knockout',
        'jQuery',
        'Angular',
      ],
      input: '',
      methodFilterList: [],
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
  watch: {
    discount(newValue, oldValue) {
      this.oldDiscount = oldValue
    },
    'organization.name': {
      handler: function(v) {
        this.sendIntercomData()
      },
      deep: true,
      immediate: true,
    },
  },
  created() {
    this.searchMethod()
  },
  methods: {
    updateDiscount() {
      this.discount = this.discount + 5
    },
    changeName() {
      this.organization.name = 'Optimized PC Innovate'
    },
    // Method for frameworkList
    searchMethod() {
      this.methodFilterList = this.frameworkList.filter(item =>
        item.toLowerCase().includes(this.input.toLowerCase())
      )
    },
  },
}
</script>

<style lang="scss">
.container {
  margin: 0 auto;
  padding: 30px;
  max-width: 600px;
  font-family: 'Avenir', Helvetica, sans-serif;
  margin: 0;
}
input {
  padding: 10px 6px;
  margin: 20px 10px 10px 0;
}
.output {
  font-size: 16px;
}
a {
  display: inline-block;
  background: rgb(235, 50, 50);
  border-radius: 10px;
  font-size: 14px;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
}
</style>
