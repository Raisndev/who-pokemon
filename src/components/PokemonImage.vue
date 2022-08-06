<template>
  <img class="pk__img" :pk-visibility="pkVisibility" :src="imgSrc" alt=""> 
</template>

<script>
export default {
    data() {
      return {
        pkVisibility: false
      }
    },
  props:{
    pokemonId:{
      type: Number,
      required: true
    },
    showPokemon:{
      type:Boolean,
      required:true,
      default: false
    }
  },
  computed:{
    imgSrc(){
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${ this.pokemonId }.svg`
    }
  },
  watch:{
    showPokemon (value, oldValue){
      if (value == true){
        this.pkVisibility = true
        console.log('ji')
      }else{
        this.pkVisibility = false
      }
    } 
  }
}
</script>

<style scoped>
.pk__container{
  height: 200px;
}.pk__img{
  height: 200px;
  filter: brightness(0);
  transition:all .5s ease;
  user-select: none;
  -webkit-user-drag: none;
}

.pk__img[pk-visibility="true"]{
  filter: brightness(1);
  transition:all .5s ease;
}
</style>