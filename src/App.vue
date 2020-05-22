<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/pokelogo.png">
    <h1>PokeGuía</h1>
    <label>Nombre:</label>
    <input type="text" v-model='pokemon.name'>
    <button @click='search'>Buscar</button>
    <div>
     <img :src="pokeImg">
    </div>
 
    <h2>Movimientos</h2>
    <ol>
      <li v-for=" move in pokeMoves" :key="move">{{move.move.name}}</li>
    </ol>
    <h2 class="ability">Habilidades</h2>
    <ol>
      <li v-for="abilitie in  pokeAbilities" :key="abilitie">{{abilitie.ability.name}}</li>
    </ol>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        pokemon: {
          name: 'pikachu',
          moves: [],
          abilities: [],
        }
      }
    },
    methods: {
      search() {
        let name = this.pokemon.name.toLowerCase()
        fetch(`http://pokeapi.co/api/v2/pokemon/${name}`)
          .then(response => response.json())
          .then(response => this.pokemon = response)
      }
    },
    created() {
      this.search()
    },
    computed: { 
        pokeImg(){
            return this.pokemon.sprites.front_default;
        },
        pokeMoves(){
          return this.pokemon.moves;
        },
        pokeAbilities(){
          return this.pokemon.abilities;
        }

       
      }
     }
  
</script>


<style>
  #app {
    text-align: center;
    margin: 30px;
    background: rgb(255, 226, 228);
    padding-bottom: 30px;
  }

  img {
    padding-top: 20px;
    margin: 0, auto;
    width: 50vh;
  }

  label {
    margin-right: 10px;
  }
  input {
    width: 30%;
    padding: 10px;
    border: none;
    margin-right: 10px;
  }
  button {
    padding: 10px;
    border: none;
    background: rgb(247, 91, 151);
    color: #fff;
  }


</style>