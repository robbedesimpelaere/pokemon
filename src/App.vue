<template>
  <logo />

  <div class="o-grid">
    <loadingSkeletons v-if="loading"> </loadingSkeletons>
    <pokemon v-else v-for="pokemon in pokemons" :pokemonData="pokemon" :key="pokemon.name"> </pokemon>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import logo from './components/Logo.vue';
import pokemon from './components/Pokemon.vue';
import loadingSkeletons from './components/loadingSkeletons.vue';
import { LucidePersonStanding } from 'lucide-vue-next';

const pokemons = ref([]);

const getPokemons = async function (limit = 12) {
  const data = await fetch(`https://pokeapi.co/api/v2/pokemon?limit=${limit}&offset=0`).then((r) => r.json());
  console.log(data);
  pokemons.value = data.results;
  //loading.value = false;
};

const loading = ref(true);

getPokemons();
</script>

<style lang="scss">
html {
  color: #fefefe;
  background: #303030;
  font-family: 'Work Sans', sans-serif;
}

.o-grid {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  max-width: 72rem;
  gap: 2rem;
  margin: 0 auto;
  padding: 2rem;
}
</style>
