<template>
  <div class="evolutions-container">
    <div class="evolutions" v-for="(evolution, index) in this.chain" v-bind:key="index">
      <div class="unit-evolution">
        <h1 class="evo-name">{{ evolution.name }}</h1>
        <img class="evo-image" :src="evolution.sprites.front_default" alt="evo-img">
        <button class="chose-btn" v-on:click="this.changeFunction(evolution)">Escolho você!</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
        chain: Array,
        changeFunction: Function,
    },
}
</script>

<style>
  .evolutions-container {
    align-items: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 50px;
    width: 90%;
  }

  .unit-evolution {
    align-items: center;
    background-color: rgba(255, 255, 255, 0.4);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    margin: 5px;
    padding: 10px;
  }

  .evo-name {
    font-family: 'TheGoodMonolith', sans-serif;
    text-transform: capitalize;
  }
  
  .evo-image {
    width: 150px;
  }

  .chose-btn {
    border: none;
    background-color: rgb(221, 3, 14);
    border-radius: 5px;
    color: white;
    font-family: 'TheGoodMonolith', sans-serif;
    font-size: 1.1em;
    font-weight: 600;
    padding: 8px;
  }

  @media (max-width: 699px) {
    .evolutions {
      width: 90%;
    }
  }

  @media (min-width: 700px) {
    .evolutions-container {
      flex-direction: row;
      flex-wrap: wrap;
      width: 50%;
  }
}
</style>