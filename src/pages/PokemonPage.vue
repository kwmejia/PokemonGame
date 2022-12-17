<template>
  <h1 v-if="!pokemon">Espere por favor ...</h1>
  <div v-else>
    <h1>¿Quién es este pokémon?</h1>
    <PokemonImage :pokemon-id="pokemon.id" :show-pokemon="showPokemon" />
    <PokemonOptions :pokemons="pokemonArr" @selection="chekAnswer($event)" />
    <template v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button @click="newGame">Nuevo Juego</button>
    </template>
  </div>
</template>

<script>
import PokemonImage from "@/components/PokemonImage.vue";
import PokemonOptions from "@/components/PokemonOptions.vue";
import getPokemonOptions from "@/helpers/getPokemonOptions.js";

export default {
  name: "PokemonPage",
  components: {
    PokemonImage,
    PokemonOptions,
  },

  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: " ",
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArr[rndInt];
    },
    chekAnswer(id) {
      this.showPokemon = true;
      if (id === this.pokemon.id) {
        this.message = `Correcto, ${this.pokemon.name} `;
      } else {
        this.message = `Oops, era ${this.pokemon.name} `;
      }
      this.showAnswer = true;
    },
    newGame() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonArr = [];
      this.pokemon = null;
      this.mixPokemonArray();
    },
  },
  mounted() {
    this.mixPokemonArray();
  },
};
</script>

<style  lang="scss" src="@/scss/main.scss">
</style>