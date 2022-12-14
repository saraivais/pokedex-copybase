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

<script>
import devtools from '@vue/devtools';
import PokemonNotFound from './components/PokemonNotFound.vue';
import PokemonDisplay from './components/PokemonDisplay.vue';
import EvolutionChain from './components/EvolutionChain.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
  export default {
    data() {
        return {
            pokemonName: "",
            evolutionUrl: "",
            searchError: false,
            chosenPokemon: {},
            evolutionChain: {},
            pokemonToDisplay: '',
            readyToDisplay: false,
            evolutions: [],
        };
    },
    methods: {
        async getEvolutions() {
          const apiResult = await fetch(this.evolutionUrl);
          const pokemonEvol = await apiResult.json();
          return pokemonEvol;
        },

        async displayPokemon(pokeId) {
          const apiResult = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokeId}`);
          const thisPokemon = await apiResult.json();
          return thisPokemon;
        },

        flattenEvoChain(obj) {
          console.log('evolution chain', obj);
          const newChain = [];
          let chain = obj.chain;
          do {
            newChain.push(chain.species.name);
            if (chain.evolves_to.length > 2) {
              newChain.push(...chain.evolves_to.map(({ species }) => species.name));
              break;
            }
            chain = chain.evolves_to[0];
          } while (chain && chain.evolves_to);
          return newChain;
        },

        async fetchAllEvolutions(pokemon) {
          const allEvoObjects = await Promise.all(pokemon.map((pokemon) => this.getPokemonDisplayInfo(pokemon)));
          return allEvoObjects;
        },
        
        async getPokemonDisplayInfo(name) {
          const apiResult = await fetch(`https://pokeapi.co/api/v2/pokemon/${name}`);
          const thisPokemon = await apiResult.json();
          return thisPokemon;
        },

        async getAllPokemonInfo() {
          this.readyToDisplay = false;
            const searchResult = await this.searchPokemon();
            this.evolutionUrl = searchResult.evolution_chain.url;
            const evolutionInfo = await this.getEvolutions();
            this.evolutionChain = this.flattenEvoChain(evolutionInfo);
            this.evolutions = await this.fetchAllEvolutions(this.evolutionChain);
            const display = await this.displayPokemon(searchResult.id);
            this.chosenPokemon = searchResult;
            this.pokemonToDisplay = display;
            this.pokemonName = "";
            this.readyToDisplay = true;
        },

        async searchPokemon() {
            try {
                const url = `https://pokeapi.co/api/v2/pokemon-species/${this.pokemonName.toLowerCase()}`;
                const apiResult = await fetch(url);
                const result = await apiResult.json();
                this.searchError = false;
                return result;
            }
            catch (err) {
                console.log(err);
                this.searchError = true;
                this.evolutionChain = {};
            }
        },

        setDisplayPokemon(pokeObject) {
          this.pokemonToDisplay = pokeObject;
        },
    },
    components: { PokemonNotFound, PokemonDisplay, EvolutionChain, HeaderComponent, FooterComponent },
}
</script>

<style>

.pokedex-container {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}

.display-area {
  align-items: center;
  display: flex;
  flex-direction: column;
  margin: 0 40px;
  width: 100vw;
}

.search-area {
  align-items: center;
  background-color: rgba(39, 100, 180, 0.5);
  border-radius: 10px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  margin: 10px;
}

.search-input {
  border: none;
  border-radius: 5px;
  font-family: 'TheGoodMonolith', sans-serif;
  font-size: 1.2em;
  margin: 5px;
  padding: 8px;
  width: 80%;
}

.search-btn {
  background-color: rgb(221, 3, 14);
  border: none;
  border-radius: 5px;
  color: white;
  font-family: 'TheGoodMonolith', sans-serif;
  font-size: 1.5em;
  font-weight: 600;
  margin: 5px;
  padding: 5px;
  text-transform: uppercase;
  width: 80%;
}

@media (min-width: 500px) {
  .search-area {
    width: 60vw;
  }
}

@media (min-width: 700px) {
  .search-area {
    padding: 20px;
    width: 50vw;
  }

  .display-area {
    flex-direction: row;
  }
}
</style>
