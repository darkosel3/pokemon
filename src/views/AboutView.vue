<script setup>
import { useRoute } from "vue-router";
import { reactive, toRefs } from "vue";
// import { data } from "autoprefixer";
const route = useRoute();
const state = reactive({
  pokemon: null,
});

fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
  .then((res) => res.json())
  .then((data) => {
    state.pokemon = data;
    console.log(state.pokemon);
  });

const { pokemon } = toRefs(state);
</script>

<template>
  <div
    class="w-3/12 m-auto flex flex-col items-center mt-8 bg-purple-100 shadow-2xl justify-center"
  >
    <h1 v-if="pokemon && pokemon.forms" class="font-bold">
      {{ pokemon.forms[0].name.toUpperCase() }}
    </h1>
    <div class="flex">
      <img class="w-48" :src="pokemon.sprites.front_shiny" alt="" />
      <img class="w-48" :src="pokemon.sprites.back_shiny" alt="" />
    </div>
    <h3 class="text-yellow-400">Types</h3>
    <div v-for="(type, idx) in pokemon.types" :key="idx">
      <h5 class="text-blue-900">{{ type.type.name }}</h5>
    </div>
  </div>
</template>

<style></style>
