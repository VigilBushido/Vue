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
          placeholder="Search with method"
          v-model="input"
          @keyup="searchMethod"
        />

        <ul>
          <li v-for="(item, i) in methodFilterList" :key="i">{{ item }}</li>
        </ul>
      </div>

      <div class="col">
        <input
          type="text"
          placeholder="Search with computed"
          v-model="input2"
        />

        <ul>
          <li v-for="(item, i) in computedList" :key="i">{{ item }}</li>
        </ul>
      </div>

      <div class="col">
        <input type="text" placeholder="Search with watcher" v-model="input3" />

        <ul>
          <li v-for="(item, i) in watchFilterList" :key="i">{{ item }}</li>
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
        employees: ['Sergio', 'John', 'Omar'],
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
      // Computed
      input2: '',
      // Watcher
      input3: '',
      watchFilterList: [],
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
    //using computed prop to do searchMethod
    computedList() {
      return this.frameworkList.filter(item => {
        return item.toLowerCase().includes(this.input2.toLowerCase())
      })
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
    //watchers vs computed props vs methods
    input3: {
      handler() {
        this.watchFilterList = this.frameworkList.filter(item =>
          item.toLowerCase().includes(this.input3.toLowerCase())
        )
      },
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
      this.organization.name = 'Optimized PC Innovations'
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
.col {
  width: 33%;
  height: 100%;
  float: left;
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
