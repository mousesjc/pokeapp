<template>
  <v-app>
    <v-app-bar app color="purple" dark>
      <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer" />
      <v-app-bar-title dark>Pokemons</v-app-bar-title>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" top temporary>
      <v-list>
        <v-list-item v-for="item in items" :key="item.title" :to="item.value">
          {{ item.title }}
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <!-- Sizes your content based upon application components -->
    <v-main>
      <!-- Provides the application the proper gutter -->
      <v-container fluid>
        <!-- If using vue-router -->
        <router-view />
      </v-container>
    </v-main>
    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<script setup>
import { reactive, provide } from "vue";

const state = reactive({
  pokemons: [],
  urlIdLookup: {},
});

fetch("https://pokeapi.co/api/v2/pokemon?limit=40")
  .then((res) => res.json())
  .then((data) => {
    console.log(data);
    state.pokemons = data.results;
    state.urlIdLookup = data.results.reduce(
      (acc, cur, idx) => (acc = { ...acc, [cur.name]: idx + 1 }),
      {}
    );
  });

provide("state", state);
</script>
<script>
export default {
  data: () => ({
    drawer: false,
    group: null,
    items: [
      {
        title: "Home",
        value: "/",
      },
      {
        title: "About",
        value: "/about/1",
      },
    ],
    oldpokemons: ["picachu"],
  }),
  watch: {
    group() {
      this.drawer = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
