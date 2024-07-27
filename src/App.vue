<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div class="p-13 mt-10 flex justify-center">
    <RouterLink class="text-amber-500 font-bold text-xl" to="/"
      >Pokemon Picker</RouterLink
    >
  </div>

  <RouterView />
</template>

<style scoped></style>
