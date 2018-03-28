<template>
  <section>
    <h1>
      Boodschappenlijstje
    </h1>
    <p>
      Voeg jouw boodschappen toe
    </p>
    <input v-model="newItem" placeholder="Boodschappen">
    <button v-on:click="addItem">Toevoegen</button>
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
export default {
  name: 'Home',
  data: () => ({
    items: [
      { message: 'Sinaasappelsap' },
      { message: 'Broodjes' }
    ]
  }),
  methods: {
    addItem: function () {
      this.items.push({ message: this.newItem })
    }
  }
}
</script>

<style lang="scss">
@import 'src/assets/scss/style.scss';

h1, h2, h3 {
  font-family: 'Signika', sans-serif;
  color: $headings;
}
p {
  color: $text;
}
.notepad {
  background: $white;
  width: 280px;
  height: 400px;
  box-shadow: 4px 4px 15px 0px rgba(0,0,0,0.35);
  margin: 50px 0;
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
