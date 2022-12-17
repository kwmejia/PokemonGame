<template>
  <div class="options-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id)"
      >
        {{ pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "PokemonOptions",
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
};
</script>
<style  lang="scss" src="@/scss/main.scss">
</style>