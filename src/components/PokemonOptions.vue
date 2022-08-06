<template>
  <div class="options container">
      <ul>
          <li v-for="pokemon in pokemons" :key="pokemon.id" @click="$emit( 'selection', pokemon.id )"> {{ pokemon.name }} </li>
      </ul>
  </div>
</template>

<script>
export default {
    props: {
      pokemons:{
        type:Array,
        required:true
      }
    }
}
</script>

<style scoped>
ul{
  list-style: none;
  margin: 0%;
  padding: 0%;
}
li{
  padding: 10px;
  border: 1px solid black;
  border-radius: 5px;
  margin: 10px;
  text-transform: capitalize;
}
</style>