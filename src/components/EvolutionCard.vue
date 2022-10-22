<script>
import axios from "axios";
export default {
  props: { pokemonEvolution: String },
  data() {
    return {
      evolution: "",
    };
  },
  methods: {
    searchEvolution(pokemonEvolution) {
      const message = this.$refs.inputField.value;
      this.message = `${message.toLowerCase()}`;
      this.evolution = axios
        .get(`https://pokeapi.co/api/v2/pokemon/${pokemonEvolution}`)
        .then(
          (response) =>
            (this.pokemon = console.log("pokemon info:", response.data.species))
        );

      this.pokemonData = axios
        .get(`https://pokeapi.co/api/v2/pokemon/${this.message}`)
        .then((response) => (this.pokemonData = response.data));
    },
  },
};
</script>
<template>
  <div>
    <PokemonCard
      v-if="`${pokemonEvolution ? searchEvolution : 0}`"
      :pokemonImage="`${pokemonData?.sprites?.front_default}`"
      :pokemonName="`${pokemonData?.name}`"
      :pokemonSpecies="`${pokemonData?.species?.url}`"
    />
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
