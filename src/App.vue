<template>
  <div id="app">
    <Header v-bind:title="this.title"/>
    <Main
        v-bind:items="this.items"
        v-on:add-item="addItem"
        v-on:delete="deleteItem"
        v-on:toggle="update"
        v-on:update="update"
    />
    <Footer/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'
import Footer from './components/Footer.vue'
import axios from 'axios';

const URL = 'api/';

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer
  },
  data: () => ({
    title: 'Apprenticeship roadmap',
    items: []
  }),
  created() {
    axios.get(URL)
      .then(list => {
        this.items.push(...list.data.sort((a, b) => a.title > b.title).sort((a, b) => a.completed > b.completed));
      })
      .catch(err => console.error(err));
  },
  methods: {
    addItem(item) {
      axios.post(`${URL}add/`, {
        title: item
      })
      .then(res => {
          this.items = [res.data, ... this.items];
      })
      .catch(err => {
        console.log(err);
      });
    },
    deleteItem(id) {
      axios.delete(`${URL}${id}`)
      .then(() => {
        this.items = this.items.filter(e => e._id !== id);
      })
      .catch(err => console.log(err));
    },
    update(item) {
      axios.post(`${URL}update/${item._id}`, {
        title: item.title,
        completed: item.completed
      })
      .then(() => {
        const index = this.items.findIndex(e => e._id === item._id);
        this.items[index].completed = !this.items[index].completed;
        this.items[index].title = item.title;
        this.items.splice(index, 1);
        if (item.completed)
          this.items = [... this.items, item];
        else
          this.items = [item, ... this.items];
      })
      .catch(err => console.log("Oops", err));
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
  }

  html {
    max-height: 100vh;
    height: 100%;
  }

  body {
    margin: 0;
    min-width: 300px;
    height: 100%;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradient 15s ease infinite;
    display: flex;
  }

  @keyframes gradient {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }

  #app {
    font-family: 'Roboto', Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: white;
    display: grid;
    grid-template-rows: 75px 1fr 75px;
    max-height: 100%;
    max-width: 800px;
    margin: 0 auto;
    flex: 1;
  }
</style>
