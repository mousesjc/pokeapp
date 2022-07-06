<template>
  <div v-if="state.pokemon">
  <pokemonCard :state="state" ></pokemonCard>
  </div>
</template>

<script setup>
import { useRoute } from "vue-router";
import { reactive } from "vue";
import pokemonCard from '@/components/pokemonCard.vue'

const route = useRoute();

const state = reactive({
  pokemon: null,
});

fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
  .then((res) => res.json())
  .then((data) => {
    console.log(data);
    state.pokemon = data;
  });
</script>
