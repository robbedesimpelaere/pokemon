<script></script>

<template>
  <div class="c-pokemon">
    <img :src="getPokemonImageUrl()" :alt="`avatar van ${pokemonData.name}`" />
    <div class="c-pokemon__info">
      <header class="c-pokemon__header">
        <h2 class="c-pokemon__name">
          {{ pokemonData.name }}
        </h2>

        <label class="c-pokemon-spin" for="">
          <input class="c-pokemon-spin__input" type="checkbox" name="" id="" />

          <RotateCcw class="c-pokemon-spin__icon" />
          <RotateCw class="c-pokemon-spin__icon" />
        </label>
      </header>
      <p class="c-pokemon__info">more info <ChevronRight /></p>
    </div>
  </div>
</template>

<script setup>
import { RotateCcw, RotateCw, ChevronRight } from 'lucide-vue-next';

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
</script>
