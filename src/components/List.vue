<template>
  <div class="col-4 col-filtered">
    <div class="card text-center w-100 mb-2 pb-2 px-3" :class="{ 'active-card': props.name.name === props.selectedPokemon.name }">
      <p class="text-capitalize mb-2">{{ props.name.name }}</p>
      <img
        :src="svgAPI + props.name.url.split('/')[6] + '.svg'"
        height="80"
      >
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps(['name', 'svgAPI', 'selectedPokemon'])
</script>

<style scoped>
.col-4 {
  width: 197px;
  height: 130px;
}
.col-filtered {
  padding-left: 8px;
  padding-right: 8px;
  padding-bottom: 8px;
}
.card {
  background-color: var(--c-grey);
  cursor: pointer;
}
.card:hover {
  border-color: var(--c-light-orange);
  background-color: var(--c-light-orange);
  transition: 0.1s ease-in-out;
}
.active-card {
  border: 2px solid var(--c-orange);
  background-color: var(--c-light-orange);
}
</style>