<script></script>

<template>
  <div class="c-pokemon">
    <img :src="getPokemonImageUrl()" :alt="`avatar van ${pokemonData.name}`" class="c-pokemon__image" />
    <div class="c-pokemon__info">
      <header class="c-pokemon__header">
        <h2 class="c-pokemon__name">
          {{ pokemonData.name }}
        </h2>

        <label class="c-pokemon-spin" :for="pokemonData.name">
          <input class="c-pokemon-spin__input" type="checkbox" :id="pokemonData.name" v-model="showBack" />

          <RefreshCcw v-if="showBack" class="c-pokemon-spin__icon" />
          <RefreshCw v-else class="c-pokemon-spin__icon" />
        </label>
      </header>
      <p class="c-pokemon__link">more info <ChevronRight /></p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { RefreshCcw, RefreshCw, ChevronRight } from 'lucide-vue-next';

const props = defineProps({
  pokemonData: {
    type: Object,
    required: true,
  },
});

const showBack = ref(false);

const getPokemonId = function () {
  const pokemonId = props.pokemonData.url.split('/')[props.pokemonData.url.split('/').length - 2];
  console.log(props.pokemonData.url, pokemonId);
  return pokemonId;
};

const getPokemonImageUrl = function () {
  const baseUrl = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/`;
  if (showBack.value) {
    return `${baseUrl}back/${getPokemonId()}.gif`;
  } else {
    return `${baseUrl}${getPokemonId()}.gif`;
  }
};
</script>

<style lang="scss">
.c-pokemon {
  width: 100%;

  &__info {
    display: flex;
    flex-direction: column;
    background-color: #444;
    color: #fff;
    padding: 0.5rem 1rem;
    border-radius: 1rem 2rem 1rem 2rem;
  }

  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__name {
    font-size: 1.5rem;
    font-weight: 600;
    margin: 0;

    &::first-letter {
      text-transform: uppercase;
    }
  }
  &-spin {
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    background-color: #111;
    border-radius: 50%;
    height: 3rem;
    width: 3rem;
    cursor: pointer;
    margin-left: 1rem;
    transition: background 0.2s ease-in-out;
    color: #fff;
    &:focus {
      background: #fff;
      color: #000;
    }
    &:hover {
      background: #808080;
    }

    &__input {
      display: none;
    }
  }
  &__image {
    height: 7rem;
    width: auto;
    display: block;
    margin-bottom: -0.5rem;
  }
  &__link {
    display: flex;
    padding: 1rem;
    font-size: 0.75rem;
    gap: 0.5rem;
    align-items: center;
    margin: 0 0 0 auto;
    text-decoration: underline;
  }
}

@media (min-width: 480px) {
  .c-pokemon {
    width: calc((100% - 1 * 2rem) / 2);
  }
}

@media (min-width: 992px) {
  .c-pokemon {
    width: calc((100% - 3 * 2rem) / 4);
  }
}
</style>
