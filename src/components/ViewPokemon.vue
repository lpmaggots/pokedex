<template>
  <div class="sticky-top space-top">
    <div class="card card-view card-scroll scroll-custom" :class="hasSelected() ? 'card-border-colored' : null">
      <div :class="hasSelected() ? null : 'd-none'">
        <button @click="clearSelected()" class="btn-close bg-light mt-2 mx-2"></button>
      </div>
      <img
        v-if="hasSelected()"
        :src="svgAPI + props.pokemon?.species?.url.split('/')[6] + '.svg'"
        class="mt-3"
        height="200"
      >
      <div class="card-body" :class="hasSelected() ? null : 'd-flex'">
        <section v-if="hasSelected()">
          <h5 class="card-title text-center text-capitalize">{{ pokemon.name }}</h5>
          <hr>
          <section class="row mb-3">
            <div class="col">
              <h5>Main data</h5>
              <p class="mb-1">
                <strong>Number:</strong> <span>{{ pokemon.order }}</span>
              </p>
              <p class="mb-1">
                <strong>Experience:</strong> <span>{{ pokemon.base_experience }}</span>
              </p>
              <p class="mb-1">
                <strong>Height:</strong> <span>{{ pokemon.height }}</span>
              </p>
              <p class="mb-1">
                <strong>Weight:</strong> <span>{{ pokemon.weight }}</span>
              </p>
              <h5 class="mt-3">Type</h5>
              <ul>
                <li v-for="type in pokemon.types" :key="type.slot" class="text-capitalize mb-0">
                  {{ type.type.name }}
                </li>
              </ul>
            </div>
            <div class="col">
              <h5>Abilities</h5>
              <ul>
                <li v-for="ability in pokemon.abilities" :key="ability.name" class="text-capitalize mb-0">
                  {{ ability.ability.name }}
                </li>
              </ul>
            </div>
          </section>
          <section class="row">
            <div class="col-12">
              <h5>Status</h5>
              <RadarChart :chart-data="chartData" :chart-options="chartOptions" class="mb-3"/>
            </div>
          </section>
        </section>
        <section v-else :class="Object.keys(props.pokemon).length == 0 ? 'w-100 d-flex flex-column justify-content-center align-items-center' : null">
          <h5 class="card-title text-muted mb-0">Select a Pokémon on the side</h5>
          <i class="mdi mdi-magnify text-muted custon-magnify"></i>
        </section>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, defineProps, defineEmits  } from 'vue'
// plugin
import { RadarChart } from "vue-chart-3"
import { Chart, registerables } from "chart.js"

const props = defineProps(['pokemon', 'svgAPI'])
const emit = defineEmits(['clear-selected'])

const hasSelected = () => {
  if(Object.keys(props.pokemon).length == 0)
  return false
return true
}

const clearSelected = () => {
  emit('clear-selected')
}

Chart.register(...registerables)
let stats = ref()

stats = props.pokemon.stats

const chartData = ref({
  labels: [],
  datasets: [
    {
      label: "Pokémon Stats",
      data: [],
      backgroundColor: "rgba(255, 165, 0, 0.2)",
      borderColor: "rgba(255, 165, 0, 1)",
      borderWidth: 2
    }
  ]
})

const chartOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
  scales: {
    r: {
      beginAtZero: true,
      angleLines: {
        color: "rgba(255, 255, 255, 0.2)"
      },
      grid: {
        color: "rgba(255, 255, 255, 0.2)"
      }
    }
  }
})

watch(() => props.pokemon, (newPokemon) => {
  if (newPokemon && newPokemon.stats) {
    chartData.value.labels = newPokemon.stats.map(stat => stat.stat.name.replace("-", " "))
    chartData.value.datasets[0].data = newPokemon.stats.map(stat => stat.base_stat)
  }
}, { deep: true, immediate: true })

</script>

<style scoped>
.card-border-colored {
  border: 2px solid var(--c-orange);
  transition: 0.1s ease-in-out;
}
hr {
  color: var(--c-orange);
}
.card-view {
  background-color: var(--c-grey);
}
.custon-magnify {
  font-size: 6rem;
}
</style>