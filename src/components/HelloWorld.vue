<template>
<v-card max-width="400" class="mx-auto" color="">
<div>
 <v-text-field hint="'Enter text to search'" placeholder="pichachu" variant="outlined" type="text" v-model="searchText" />
 </div>

  <v-btn v-for="poke in searchResult" :key="poke.name" variant="text">
    <router-link :to="`/about/${state.urlIdLookup[poke.name]}`">
      {{ poke.name }}
    </router-link>
  </v-btn>

  </v-card>
</template>
<script>
export default {
  data() {
    return {
      searchText: '',
    }
  },
  computed: {
    searchResult() {
      if (this.searchText === '') {
        return []
      } else {
        return this.state.pokemons.filter(pokemon => pokemon.name.includes(this.searchText))
      }
    } 
  },
  inject: {
    state: 'state'
  }
}</script>

