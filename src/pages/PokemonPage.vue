<template>
   <h1 v-if="!pokemon">Espere por favor...</h1>

   <div v-else="pokemon">
      <h1>¿Quién es este Pokemon?</h1>

         <PokemonPicture 
            :pokemonId="pokemon.id" 
            :showPokemon= "showPokemon"/>
         <PokemonOptions 
            :pokemons="pokemonArr"
            @selection="checkAnswer"/> 
   </div>
   


</template>

<script>
   import PokemonOptions from '../components/PokemonOptions.vue'
   import PokemonPicture from '../components/PokemonPicture.vue'

   import getPokemonOptions from '../helpers/getPokemonOptions'

   //console.log(getPokemonOptions())

export default {
    components: { PokemonOptions, PokemonPicture },
    data() {
      return {
         pokemonArr:[],
         pokemon: null,
         showPokemon: false
      }
    },
    methods: {
      async mixPokemonArr () {
        this.pokemonArr = await getPokemonOptions()

        const rdnInt = Math.floor( Math.random() * 4)
        this.pokemon = this.pokemonArr[rdnInt]
      },
      checkAnswer(pokemonId) {
         this.pokemon = true
      }
    }, 
    mounted() {
      this.mixPokemonArr()
    }
}
</script>


