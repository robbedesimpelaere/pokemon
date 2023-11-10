<template>
  <logo />

  <h1>Pokemon!</h1>

  <div>
    <pokemon v-for="pokemon in pokemons"
     :pokemonData="pokemon" 
     :key="pokemon.name"
     > 
    </pokemon>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import logo from './components/Logo.vue';
import pokemon from './components/Pokemon.vue';

const pokemons = ref([]);

const getPokemons = async function (limit = 12) {
  const data = await fetch(`https://pokeapi.co/api/v2/pokemon?limit=${limit}&offset=0`).then((r) => r.json());
  console.log(data);
  pokemons.value = data.results;
};

getPokemons();
</script>

<style lang="scss">
html {
  color: #fefefe;
  background: #303030;
  font-family: 'Work Sans', sans-serif;
}
</style>
