<template>
    <div id="app">
      <div class="column is-half is-offset-one-quarter is-desktop content is-centered is-vcentered">
        <img src="./assets/1.png" >
        <img src="./assets/3.png" >
        <hr>
        <h4 class="is-size-4 has-text-centered">Pokedex</h4>
        <input type="text" class="input is-rounded" placeholder="Buscar pokemon pelo nome..." v-model="busca">
        <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar"><b>Buscar</b></button>
        <div v-for="(poke,index) in filteredPokemons" :key="poke.url" class= "is-centered is-vcentered" >
          <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />        
        </div>
      </div>
      
    </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'
export default {
  name: 'App',

  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },

  created: function(){
   axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
     console.log("Pegou a lista de pokemons!")
     this.pokemons = res.data.results
     this.filteredPokemons = res.data.results

     
   })
  },
  components:{
    Pokemon
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.toLowerCase() == this.busca.toLowerCase())//metodo Utilizado para colocar os nomes em letras minusculas
      }
    }
  }
  // computed: {
  //   resultadoBusca: function() {
  //     if(this.busca == '' || this.busa == ' ')
  //   }
  // }  
}
</script>

<style>

#buscaBtn {
  margin-top: 2%,
}

</style>
