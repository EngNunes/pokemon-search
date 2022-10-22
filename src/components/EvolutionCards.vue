<script>
import axios from "axios";

export default {
  props: { pokemonUrl: String },
  data() {
    return {
      evolutionsChain: "",
      evolutions: "",
      evolution: "",
    };
  },
  methods: {
    async handleEvolutionCards(evolutionKey) {
      this.evolution = axios
        .get(evolutionKey)
        .then(
          (response) =>
            (this.evolution = axios
              .get(response?.data?.evolution_chain?.url)
              .then(
                (response) =>
                  (this.evolution =
                    response?.data?.chain?.evolves_to[0].species.name)
              ))
        );
    },
  },
};
</script>
<template>
  <button @click="handleEvolutionCards(pokemonUrl)">Pesquisar Evolução</button>
  <div v-if="`${evolution}`">
    <H1>Evolução</H1>
    <p>{{ evolution }}</p>
  </div>
</template>
