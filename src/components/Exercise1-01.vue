<template>
  <section>
    <!--- So it can contain multiple div elements -->
    <div class="Lifecycle">
      <h1>Vue Lifecycle hooks</h1>
      <ul>
        <li v-for="(item, n) in list" :key="n">
          {{ item }} <b @click="deleteItem(item)">Delete</b>
        </li>
      </ul>
    </div>

    <div class="ReturnMethods">
      <h1>Returning Methods</h1>

      <div>Cart({{ totalItems }}) {{ formatCurrency(totalCost) }} </div>
      <ul>
        <li v-for="n in 5" :key="n">
          <a href="#" @click="addToCart(n)">Add {{ formatCurrency(n) }}</a>
        </li>
      </ul>
    </div>

    <h1 v-show="true" v-once v-text="text">Loading...</h1>
    <h2 v-show="false" v-html="html" />
    <h3>Looping through arrays</h3>
    <ul>
      <li v-for="n in 5" :key="n">
        {{ n }}
      </li>
    </ul>
    <ul>
      <li v-for="(item, n) in interest1" :key="n">
        {{ item }}
      </li>
    </ul>
    <a
      :href="link.url"
      :target="link.target"
      :tabindex="link.tabindex"
      v-text="link.title"
    />
    <div class="form">
      <label>
        <input type="text" v-model="name" />
      </label>
      <label>
        Preferred javascript style
        <select name="language" v-model="language">
          <option value="Javascript">JavaScript</option>
          <option value="TypeScript">TypeScript</option>
          <option value="CoffeeScript">CoffeeScript</option>
          <option value="Dart">Dart</option>
        </select>
      </label>
    </div>
    <ul class="overview">
      <li><strong>Overview</strong></li>
      <li>Name: {{ name }}</li>
      <li>Preference: {{ language }}</li>
    </ul>
    <h1> Looping through array of objects</h1>
    <ul>
      <li v-for="(item, n) in interests2" :key="n">
        {{ item.title }}
        <ol v-if="item.favorite.length > 0">
          <li v-for="(fav, m) in item.favorite" :key="m"> {{ fav }}</li>
        </ol>
      </li>
    </ul>
    <div id="Trigger">
      <h1>Triggering Vue Methods</h1>
      <ul>
        <li v-for="n in 5" :key="n">
          <a href="#Trigger" @click="triggerAlert(n)">Trigger {{ n }} </a>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  methods: {
    triggerAlert(n) {
      alert(`${n} has been clicked`)
    },
    addToCart(n) {
      this.totalItems = this.totalItems + 1
      this.totalCost = this.totalCost + n
    },
    deleteItem(value) {
      this.list = this.list.filter(item => item !== value)
    },
  },
  data() {
    return {
      list: [
        'League of Legends',
        'Clash of Clans',
        'Path of Exile',
        'Dead Space',
        'Resident Evil 4',
        'Battlefield 2',
        'Halo Wars',
        'Fallout 4',
        'BF 2042',
        'Life is Fuedal',
      ],
      // v-text
      text: 'Directive text',
      // v-html
      html: 'Stylise</br>HTML in<br/><b>your data</b>',
      // v-bind
      link: {
        url: 'https://google.com',
        target: '_blank',
        tabindex: '0',
        title: 'Go to Google',
      },
      name: '',
      language: '',
      interest1: [
        'Giannis Antekounpo',
        'Path of Exile',
        'Full Stack Java Programming',
      ],
      interests2: [
        {
          title: 'TV',
          favorite: ['Designated Survivor', 'Spongebob'],
        },
        {
          title: 'Games',
          favorite: ['CS:GO'],
        },
        {
          title: 'Sports',
          favorite: [],
        },
      ],
      totalItems: 0,
      totalCost: 0,
      formatCurrency(val) {
        return `$${val.toFixed(2)}`
      },
    }
  },
  beforeCreate() {
    console.log('beforeCreate: data is static, thats it')
  },
  created() {
    console.log('created: data and events ready, but no DOM')
  },
  beforeUpdate() {
    alert(
      'beforeUpdate: we know an update is about to happen, and have the data'
    )
  },
  updated() {
    alert('updated: virtual DOM will update after you click OK')
  },
  beforeDestroy() {
    alert('beforeDestroy: about to blow up this component')
  },
  destroyed() {
    alert('destroyed: this component has been destroyed')
  },
}
</script>

<style lang="scss" scoped>
.form {
  display: flex;
  justify-content: space-evenly;
  max-width: 800px;
  padding: 40px 20px;
  border-radius: 10px;
  margin: 0 auto;
  background: #ececec;
}

.overview {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  max-width: 300px;
  margin: 40px auto;
  padding: 40px 20px;
  border-radius: 10px;
  border: 1px solid #ececec;

  > li {
    list-style: none;
    + li {
      margin-top: 20px;
    }
  }
}

.Lifecycle {
  ul {
    padding-left: 0;
  }
  li {
    display: block;
    list-style: none;

    + li {
      margin-top: 10px;
    }
  }
  b {
    display: inline-block;
    background: rgb(235, 50, 50);
    padding: 5px 10px;
    border-radius: 10px;
    font-size: 10px;
    color: white;
    text-transform: uppercase;
    text-decoration: none;
  }
}
h2 {
  margin: 40px 0 0;
  font-weight: normal;
}
a {
  margin-top: 10px;
  display: inline-block;
  background: #4fc08d;
  border-radius: 10px;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
}
</style>
