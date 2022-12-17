<template>
  <div class="pokemon-container">
    <img :src="imgSrc" alt="pokemon" class="hidden-pokemon" />
    <img v-if="showPokemon" :src="imgSrc" alt="pokemon" class="fade-in" />
  </div>
</template>

<script>
export default {
  name: "PokemonImage",
  props: {
    pokemonId: {
      type: Number,
      required: true,
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  computed: {
    imgSrc() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
    },
  },
};
</script>

<style  lang="scss" src="@/scss/main.scss">
</style>