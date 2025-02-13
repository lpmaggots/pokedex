<template>
  <div class="container pt-4">
    <section class="row">
      <div class="col-sm-12 col-md-6">
        <div
          class="card card-scroll scroll-custom"
          ref="scrollContainer"
          @scroll="handleScroll"
        >
          <h3 class="text-center mt-3">Pokemons</h3>
          <div
            class="bg-white sticky-top mx-3 py-3"
            :class="{ 'border-teste': isScrolled }"
          >
            <div class="form-group">
              <label for="search" hidden>Search</label>
              <input
                v-model="search"
                type="text"
                id="search"
                class="form-control custom-form-control"
                placeholder="Search"
                autocomplete="off"
              >
            </div>
          </div>
          <div class="card-body">
            <section
              v-if="pokemonFiltered.length > 0"
              class="fix-margin-left"
              :class="pokemonFiltered.length > 3 && search ? 'row-filtered' : 'row'"
            >
              <List
                v-for="(pokemon, index) in pokemonFiltered"
                @click="viewPokemon(pokemon, index)"
                :key="index"
                :name="pokemon"
                :svgAPI="api.svg"
                :selectedPokemon="selectedPokemon"
              />
            </section>
            <section v-else class="w-100 text-center">
              <h6 class="card-title text-muted mb-0">No Pokémon found</h6>
            </section>
          </div>
        </div>
      </div>
      <div class="col-sm-12 col-md-6">
        <ViewPokemon
          @clear-selected="clearSelected()"
          :pokemon="selectedPokemon"
          :svgAPI="api.svg"
        />
      </div>
    </section>
  </div>
</template>

<script setup>
import { onMounted, ref, reactive, computed, watch } from 'vue'
// components
import List from '../components/List.vue'
import ViewPokemon from '../components/ViewPokemon.vue'

const api = reactive({
  pokemon: 'https://pokeapi.co/api/v2/pokemon?limit=151&offset=0',
  svg: ref('https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/')
})

let search = ref('')
let scrollContainer = ref(null)
let isScrolled = ref(false)
let pokemons = reactive({ list: [] })
let selectedPokemon = reactive({})


onMounted(() => {
  fetch(api.pokemon)
  .then(response => response.json())
  .then(response => {
    pokemons.list = response.results
  })
})

watch(search, () => {
  if(scrollContainer.value) {
    scrollContainer.value.scrollTop = 0
  }
})

const handleScroll = () => {
  if (scrollContainer.value) {
    isScrolled.value = scrollContainer.value.scrollTop > 0
  }
}

const pokemonFiltered = computed(() => {
  if(pokemons.list && search.value) {
    return pokemons.list.filter(pokemon =>
      pokemon.name.toLowerCase().includes(search.value.toLowerCase())
    )
  }
  return pokemons.list
})

const viewPokemon = (pokemon, index) => {
  fetch(pokemon.url)
  .then(response => response.json())
  .then(response => {
    Object.assign(selectedPokemon, response)
  })
}

const clearSelected = () => {
  for (const key in selectedPokemon) {
    delete selectedPokemon[key]
  }
}
</script>

<style scoped>
.border-teste {
  border-bottom: 1px solid var(--c-light-grey);
  box-shadow: 0px 3px 2px -2px var(--c-light-grey);
}
.custom-form-control {
  border: 1px solid var(--c-orange);
}
.row-filtered {
  display: flex !important;
  flex-direction: row;
  flex-wrap: wrap;
  align-content: baseline;
}
.fix-margin-left {
  margin-left: 0 !important;
}
</style>