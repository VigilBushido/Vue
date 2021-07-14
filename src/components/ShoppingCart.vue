<template>
  <div class="form">
    <label>
      <input type="text" v-model="itemToShop" />
    </label>
    <label>
      Level of Priority:
      <select name="priority" v-model="priority">
        <option value="Urgent">Urgent</option>
        <option value="Immediate">Immediate</option>
        <option value="Casual">Casual</option>
        <option value="Can Wait">Can Wait</option>
      </select>
    </label>
    <ul class="overview">
      <li><strong>Shopping List</strong></li>
      <li>Item To Buy: {{ itemToShop }}</li>
      <li>Priority Level: {{ priority }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  methods: {
    addItem(value) {
      this.shoppinglist = this.shoppinglist.add(value)
    },
    deleteItem(value) {
      this.shoppinglist = this.shoppinglist.filter(
        itemToShop => itemToShop !== value
      )
    },
  },
  data() {
    return {
      shoppinglist: [],
      itemToShop: '',
      priority: '',
    }
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
  position: absolute;
  right: 0px;
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
</style>
