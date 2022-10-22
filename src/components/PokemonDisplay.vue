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

<style>

.pokemon-container {
  align-items: center;
  background-color: rgba(255, 255, 255, 0.6);
  border-radius: 20px;
  display: flex;
  font-family: 'TheGoodMonolith', sans-serif;
  flex-direction: column;
  padding: 10px;
  width: 90%;
}

.general-info {
  align-items: center;
  display: flex;
  justify-content: space-evenly;
  width: 100%;
}

.info-number {
  font-weight: 600;
}

.pokemon-name {
  text-transform: capitalize;
}

.types-container {
  margin: 5px;
}

.type {
  border-radius: 5px;
  list-style: none;
  padding: 5px;
  font-weight: 600;
}

.bug {
  background-color: rgb(193, 196, 60);
}

.dragon {
  background-color: rgb(46, 34, 211);
}

.electric {
  background-color: rgb(250, 198, 53);
}

.fighting {
  background-color: rgb(110, 36, 18);
}

.fire {
  background-color: rgb(240, 108, 20);
}

.flying {
  background-color: rgb(156, 139, 236);
}

.ghost {
  background-color: rgb(87, 62, 202);
}

.steel {
  background-color: gray;
}

.grass {
  background-color: rgb(65, 150, 65);
}

.ground {
  background-color: rgb(228, 179, 107);
}

.dark {
  background-color: rgb(41, 28, 28);
  color: white;
}

.fairy {
  background-color: #e769e7;
}

.ice {
  background-color: rgb(125, 228, 241);
}

.normal {
  background-color: rgb(151, 133, 111);
}

.poison {
  background-color: rgb(120, 43, 184);
}

.psychic {
  background-color: rgb(240, 97, 121);
}

.rock {
  background-color: rgb(122, 75, 14);
}

.water {
  background-color: rgb(36, 132, 221);
}

.stats-container {
  font-size: 1.1em;
  width: 80%;
}

.stat {
  font-weight: 300;
}

.stat-number {
  font-weight: 600;
}

.pokemon-image {
  width: 200px;
}

@media (min-width: 500px) {
  .pokemon-container {
    width: 60%;
  }
}

@media (min-width: 700px) {
  .pokemon-container {
    width: 45%;
  }
}

</style>