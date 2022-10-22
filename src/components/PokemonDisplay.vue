<template>
  <div class="pokemon-container">
    <h1 class="pokemon-name">{{ this.pokemonObject.name }}</h1>
    <img class="pokemon-image" :src=this.pokemonObject.sprites.front_default alt="pokemon-image">
    <div class="general-info">
      <p>Height: <span class="info-number">{{ this.pokemonObject.height }}</span></p>
      <p>Weight: <span class="info-number">{{ this.pokemonObject.weight }}</span></p>
    </div>
    <ul class="types-container" v-for="({ type }, index) in this.pokemonObject.types" v-bind:key="index">
      <div :class="`type ${type.name}`">{{ type.name }}</div>
    </ul>
    <ul class="stats-container" v-for="(stat, index) in this.pokemonObject.stats" v-bind:key="index">
      <p class="stat">{{ stat.stat.name }}: <span class="stat-number">{{ stat.base_stat }}</span></p>
    </ul>
  </div>
</template>

<script>
  export default { 
    props: {
      pokemonObject: {
        name: String,
        sprites: {
          front_default: String,
        },
        stats: Array,
        weight: Number,
        height: Number,
        types: Array,
      }
    },
  }
</script>

