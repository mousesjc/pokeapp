<template>
<v-card class="mx-auto" max-width="400">
    <v-card-title class="text-h4">{{ state.pokemon.name }}</v-card-title>

    <v-container>
      <v-row>
        <v-col>
          <v-img :src="state.pokemon.sprites.front_default" />
        </v-col>
        <v-col>
          <v-img :src="state.pokemon.sprites.back_default" />
        </v-col>
      </v-row>
    </v-container>
        <v-card class="mx-auto" variant="flat" >
        <div class="text-h4">
        <v-card-title class="font-weight-light">abilities</v-card-title>
        </div>
    <v-chip dark class="ma-2" text-color="white"
      v-for="ability in state.pokemon.abilities"
      :key="ability.ability.name"
      color="purple-darken-1">{{ ability.ability.name }}</v-chip
    ></v-card>
    <v-card variant="flat">
        <v-card-title class="font-weight-light">stats</v-card-title>
    <v-table theme="light">
        <tbody v-for="stat in state.pokemon.stats" :key="stat.stat.name">
        <td class="text-center">{{ stat.stat.name }}</td>
        <td class="text-left">{{ stat.base_stat }}</td></tbody>
    </v-table>
    </v-card>
    <v-card-actions><v-btn :to="'/'">Close</v-btn></v-card-actions>
  </v-card>
  </template>

  <script setup>
  defineProps(['state'])
  </script>