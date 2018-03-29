<template>
  <section>
    <h1>
      Boodschappenlijstje
    </h1>
    <p>
      Voeg jouw boodschappen toe
    </p>
    <input class="boodschappen" v-model="newItem" placeholder="Boodschappen" type="text">
    <button type="submit" v-on:click="addItem" v-bind:disabled="(newItem === '')">Toevoegen</button>
    <div class="notepad">
      <h2>Boodschappen</h2>
      <ul>
        <li v-for="item in items" :key="item.id">
          {{ item.message }}
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import {db} from '../firebase'

export default {
  name: 'Home',
  data: () => ({
    items: [],
    newItem: ''
  }),
  firebase: {
    items: db.ref('items')
  },
  methods: {
    addItem: function (event) {
      this.$firebaseRefs.items.push({ message: this.newItem })
      this.newItem = ''
    }
  }
}
</script>

<style lang="scss">
@import 'src/assets/scss/style.scss';

section {
  margin: 40px 0;
}
h1, h2, h3 {
  font-family: 'Signika', sans-serif;
  color: $headings;
  margin: 0;
}
h1 {
  font-size: 30px;
}
p {
  color: $headings;
}
.boodschappen, button {
  font-family: inherit;
  font-size: inherit;
  border: 0;
  padding: 15px;
  width: calc(280px - 30px);
  display: block;
  margin: 0 auto;
  &:focus {
    outline: 0;
  }
}
button {
  font-family: 'Signika', sans-serif;
  font-size: 20px;
  margin: 10px auto;
  background: $headings;
  width: 280px;
  color: $white;
  &[disabled=disabled] {
    background: rgba($headings, .5);
    color: rgba($white, .8);
  }
}
.notepad {
  background: $white;
  width: 280px;
  height: 100%;
  box-shadow: 4px 4px 15px 0px rgba(0,0,0,0.35);
  margin: 50px auto;
  overflow: scroll;
  h2 {
    color: $white;
    background: $headings;
    text-align: center;
    margin: 0;
    padding: 10px 0;
  }
  ul {
    padding: 0;
    list-style: none;
    text-align: center;
    li {
      padding: 10px 0;
      border-bottom: 3px solid #EFEEED;
      &:first-child {
        padding: 0 0 10px 0;
      }
    }
  }
}
</style>
