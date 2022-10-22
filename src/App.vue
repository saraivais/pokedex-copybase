<template>
  <HeaderComponent />
  <div class="pokedex-container">
    <div class="search-area">
      <input class="search-input" type="text" v-model="pokemonName">
      <button class="search-btn" v-on:click="getAllPokemonInfo()">Buscar</button>
    </div>

    <div class="display-area">
    <PokemonDisplay v-if="readyToDisplay"
      :pokemonObject="this.pokemonToDisplay"
    />
    <div class="not-found" v-if="searchError">
      <PokemonNotFound />
    </div>

    <EvolutionChain
      v-if="readyToDisplay"
      :chain="this.evolutions"
      :changeFunction="this.setDisplayPokemon"
    />
    </div>

  </div>
  <FooterComponent />
</template>
