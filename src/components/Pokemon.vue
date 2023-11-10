<script></script>

<template>
  <p>
    {{ pokemonData.name }}
  </p>
</template>

<script setup>
const props = defineProps({
  pokemonData: {
    type: Object,
    required: true,
  },
});
</script>
