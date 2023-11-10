<script></script>

<template>
  <p>
    {{ pokemonData.name }}
  </p>
  <img :src="getPokemonImageUrl()" :alt="`foto ${pokemonData.name}`" />
</template>

<script setup>
const props = defineProps({
  pokemonData: {
    type: Object,
    required: true,
  },
});

const getPokemonId = function () {
  const pokemonId = props.pokemonData.url.split('/')[props.pokemonData.url.split('/').length - 2];
  console.log(props.pokemonData.url, pokemonId);
  return pokemonId;
};

const getPokemonImageUrl = function () {
  return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${getPokemonId()}.gif`;
};

getPokemonId();
</script>
