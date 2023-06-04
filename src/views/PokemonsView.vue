<script setup>
import { RouterLink } from "vue-router";
import { useGetData } from "@/composables/getData";

const { data, loading, getData, error } = useGetData();

getData("https://pokeapi.co/api/v2/pokemon/");
</script>

<template>
  <h1 class="mt-2">Pokemons</h1>
  <p v-if="loading">Cargando información...</p>
  <div class="alert alert-danger mt-2" v-if="error">{{ error }}</div>
  <div v-if="data">
    <ul class="list-group">
      <li v-for="poke in data.results" class="list-group-item">
        <RouterLink :to="`pokemons/${poke.name}`">
          {{ poke.name }}
        </RouterLink>
      </li>
    </ul>
    <div class="mt-4 mb-5">
      <button
        :disabled="!data.previous"
        class="button btn btn-warning me-2"
        @click="getData(data.previous)"
      >
        Previous
      </button>
      <button
        :disabled="!data.next"
        class="button btn btn-primary"
        @click="getData(data.next)"
      >
        Next
      </button>
    </div>
  </div>
</template>
