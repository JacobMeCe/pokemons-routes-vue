<script setup>
import { useRoute, useRouter } from "vue-router";
import { useGetData } from "@/composables/getData";
import { useFavoritosStore } from "@/store/favoritos";

const route = useRoute();
const router = useRouter();
const useFavoritos = useFavoritosStore();

const { add, findPoke } = useFavoritos;

const { getData, data, loading, error } = useGetData();

const back = () => {
  router.push("/pokemons");
};

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>

<template>
  <p v-if="loading">Cargando información...</p>
  <div class="alert alert-danger mt-2" v-if="error">{{ error }}</div>
  <div v-if="data">
    <h1 class="mt-2">Nombre Pokemon: {{ ($route.params.name).toUpperCase() }}</h1>
    <img :src="data.sprites?.front_default" alt="" />
    <h2> Numero pokedex: {{ data.id }} </h2>
    <p>Tipo(s):</p>
    <ul class="list-group ">
      <li class="list-group-item" v-for="(type) in (data.types)" :key="type.slot"> {{ type.type.name }} </li>
    </ul>
  </div>

  <div class="mt-4">
    <button @click=" back " class="btn btn-primary me-2">Volver</button>
    <button :disabled=" data ? findPoke(data.name) : true " class="btn btn-primary" @click="add(data)">
      Agregar Favoritos
    </button>
  </div>
</template>

<!-- -->