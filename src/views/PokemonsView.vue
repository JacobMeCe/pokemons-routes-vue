<script setup>
import axios from "axios";
import { ref } from "vue";
import { RouterLink } from "vue-router";

//https://pokeapi.co/api/v2/pokemon/
const pokemons = ref([]);
const getData = async () => {
  try {
    const { data } = await axios.get("https://pokeapi.co/api/v2/pokemon/");
    pokemons.value = data.results;
  } catch (error) {
    console.error(error);
  }
};
getData();
</script>

<template>
  <h1>Pokemons</h1>
  <ul class="list-group">
    <li class="list-group-item" v-for="poke in pokemons">
      <RouterLink :to="`pokemons/${poke.name}`">{{ poke.name }}</RouterLink>
    </li>
  </ul>
</template>
