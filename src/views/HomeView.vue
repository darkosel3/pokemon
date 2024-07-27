<script setup>
import { reactive, toRefs, computed } from "vue";

const state = reactive({
  pokemons: [],
  urlidLookup: {},
  text: "",
  filteredPokemonList: computed(() => updatePokemon()),
});

function updatePokemon() {
  if (!state.text) {
    return [];
  }
  return state.pokemons.filter((pokemon) => pokemon.name.includes(state.text));
}

fetch("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0.")
  .then((res) => res.json())
  .then((data) => {
    state.pokemons = data.results;
    state.urlidLookup = data.results.reduce(
      (acc, cur, idx) => (acc = { ...acc, [cur.name]: idx + 1 }),
      {}
    );
  });
const { pokemons, urlidLookup, text, filteredPokemonList } = toRefs(state);
</script>

<template>
  <div class="w-full flex justify-center">
    <input
      type="text"
      class="mt-10 p-2 border-blue-500 border-2"
      placeholder="Enter Pokemon here"
      v-model="text"
    />
  </div>
  <div class="p-4 flex flex-wrap flex-col items-center">
    <div
      class="text-base font-semibold text-blue-500"
      v-for="(pokemon, idx) in filteredPokemonList"
      :key="idx"
    >
      <router-link :to="`/about/${urlidLookup[pokemon.name]}`">{{
        pokemon.name
      }}</router-link>
    </div>
  </div>
</template>
