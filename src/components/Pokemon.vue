<template>
    <div id="pokemon">                     
        <div class="card">
  <div class="card-image">
    <figure >
      <img :src="currentImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">      
      <div class="media-content has-text-centered">
        <p class="title is-4">{{num}} - {{upper(name)}} </p>
        <p class="subtitle is-6">{{pokemon.type}}</p>
      </div>
    </div>

    <div class="content">
        <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar sprite</button>
    </div>
  </div>
</div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    created: function(){
        axios.get(this.url).then(res =>{
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.frontshiny = res.data.sprites.front_shiny
            this.pokemon.back = res.data.sprites.back_default
            this.pokemon.backshiny = res.data.sprites.back_shiny
            this.currentImg = this.pokemon.front
            this.currentShiny = this.pokemon.front_shiny
            console.log(this.pokemon)
        })
    },

    data(){
        return {
            isFront: true,
            currentImg:'',
            isFrontshiny: true,
            currentShiny: '',
            pokemon:{
                type:'', //Dado, só vai ser reativo se usar dentro do data
                front:'',
                frontshiny:'',
                back:'',
                backshiny:''
            }
        }
    },

  props: {
      num: Number,
      name: String,
      url: String,

  },
  methods: {
        upper: function(value){
            var newName = value[0].toUpperCase() + value.slice(1)
            return newName
        },

        mudarSprite: function(){
            if(this.isFront && this.isFrontshiny){
                this.isFront = false
                this.isFrontshiny = false
                this.currentImg = this.pokemon.back
                this.currentShiny = this.pokemon.back_shiny
            }else{
                this.isFront = true
                this.isFrontshiny = true
                this.currentImg = this.pokemon.front
                this.currentShiny = this.pokemon.front_shiny

            }
        }
    }
}
</script>

<style scoped>
#pokemon{
    margin-top: 2%;
}

</style>