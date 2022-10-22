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

