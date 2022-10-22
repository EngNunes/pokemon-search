<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>

<script>
import axios from "axios";
import PokemonCard from "./PokemonCard.vue";
export default {
  data() {
    return {
      message: "",
      pokemon: "",
      pokemonData: "",
    };
  },
  methods: {
    handleSubmit() {
      const message = this.$refs.inputField.value;
      this.message = `${message.toLowerCase()}`;
      this.pokemon = axios
        .get(`https://pokeapi.co/api/v2/pokemon/${this.message}`)
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
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      <input
        type="text"
        v-model="text"
        placeholder="digite pokemon"
        ref="inputField"
      />
      <div id="example-1">
        <button @click="handleSubmit">Pesquise</button>
        <!-- <p>você digitou {{ message }}</p>
        <p>name {{ pokemonData?.sprites?.front_default }}</p>
        <p>specie {{ pokemonData.url }}</p> -->
      </div>
      <div>
        <PokemonCard
          v-if="`${pokemon}`"
          :pokemonImage="`${pokemonData?.sprites?.front_default}`"
          :pokemonName="`${pokemonData?.name}`"
          :pokemonSpecies="`${pokemonData?.species?.url}`"
        />
      </div>
    </h3>
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
