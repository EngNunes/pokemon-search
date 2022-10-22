<script>
import EvolutionCards from "./EvolutionCards.vue";
export default {
  props: { pokemonImage: String, pokemonName: String, pokemonSpecies: String },
  components: { EvolutionCards },
};
</script>
<template>
  <div class="greetings">
    <H1>Resultado</H1>
    <img
      v-bind:src="`${pokemonImage}`"
      alt="pokemon image"
      width="125"
      height="125"
    />
    <p>{{ pokemonName }}</p>
  </div>
  <div>
    <EvolutionCards
      v-if="`${pokemonSpecies}`"
      :pokemonUrl="`${pokemonSpecies}`"
    />
  </div>
</template>


