<template>
  <section>
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
  </section>
</template>

<script>
export default {
  data() {
    return {
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
h2 {
  margin: 40px 0 0;
  font-weight: normal;
}
a {
  display: block;
  margin-top: 40px;
}
</style>
