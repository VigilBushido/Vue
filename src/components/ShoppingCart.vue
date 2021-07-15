<template>
  <div class="container">
    <h1>Shopping List</h1>
    <label>
      <input
        placeholder="Press enter to add new item"
        v-model="input"
        @keyup.enter="addItem"
        ref="input"
      /><button @click="addItem">Add item</button>
    </label>

    <label>
      Level of Priority:
      <select name="priority" v-model="priority">
        <option value="- Urgent">- Urgent</option>
        <option value="- Immediate">- Immediate</option>
        <option value="- casual">- Casual</option>
        <option value="- can Wait">- Can Wait</option>
      </select>
    </label>

    <ul class="overview">
      <li>Item To Buy: {{ input }}</li>
      <li>Priority Level {{ priority }}</li>
    </ul>

    <!--     <ul class="left">
      <strong>Official List</strong>
      <li v-for="(item, n) in shoppingList" :key="n">
        {{ item }} <b @click="deleteItem(item)">Delete</b>
      </li>
    </ul> -->
    <ul v-if="shoppingList">
      <li v-for="(item, i) in shoppingList" :key="i" class="item"
        ><span> {{ item }} {{ priority }}</span>
        <button class="button--remove" @click="deleteItem(i)">Remove</button>
      </li>
    </ul>
    <br />
    <button class="button--delete" @click="deleteItem()">Delete ALL</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: '', //itemToShop: '',
      shoppingList: [],
      priority: '',
    }
  },
  methods: {
    addItem() {
      //this.shoppingList = this.shoppingList.push(value)
      //no adding to the list if empty input
      if (!this.input) return
      this.shoppingList.push(this.input)
      //clear input afterwards
      this.input = ''
      //focus the input element for quick typing!
      this.$refs.input.focus()
    },
    deleteItem(i) {
      if (i == 0) {
        this.shoppingList = this.shoppingList.filter((item, x) => x !== i)
        console.log(this.shoppingList)
        console.log(i)
      }
      //this.shoppingList = this.shoppingList.filter(item => item !== value)

      //filter out that array item and update the shoppingList prop;
      //otherwise replace the data prop with an empty array
      else if (i != 0)
        this.shoppingList = i
          ? this.shoppingList.filter((item, x) => x !== i)
          : []
    },
  },
}
</script>

<style lang="scss">
@import 'src/styles/global';

$color-green: #4fc08d;
$color-grey: #2c3e50;

.container {
  max-width: 600px;
  margin: 80px auto;
}

.item {
  display: flex;
  justify-content: space-between;
}

// Type
.h2 {
  font-size: 21px;
}

.user-input {
  display: flex;
  align-items: center;
  padding-bottom: 20px;
  input {
    width: 100%;
    padding: 10px 6px;
    margin-right: 10px;
  }
}

.item {
  display: flex;
  align-items: center;
}

// Buttons
button {
  appearance: none;
  padding: 10px;

  font-weight: bold;
  border-radius: 10px;
  border: none;
  background: $color-grey;
  color: white;
  white-space: nowrap;

  + button {
    margin-left: 10px;
  }
}

.button--delete {
  display: block;
  margin: 0 auto;
  background: red;
}

.button--remove {
  background: none;
  color: red;
  text-transform: uppercase;
  font-size: 11px;
  align-self: flex-end;
}

ul {
  display: block;
  margin: 0 auto;
  padding: 30px;
  border: 1px solid rgba(0, 0, 0, 0.25);

  > li {
    color: $color-grey;
    margin-bottom: 4px;
  }
}
</style>
