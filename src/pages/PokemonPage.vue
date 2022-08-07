<template>
	<h1 v-if="!pokemon">Analizando Pokemones</h1>

	<div v-else>
		<h1>Que pokemon es?</h1>
		<PokemonImage :pokemonId="pokemon.id" :showPokemon="showPokemon" />
		<PokemonOptions :pokemons="pokemonArr" @selection="checkAnswer($event)" />
		<template v-if="showAnswer">
			<h2>{{ message }}</h2>
			<button @click="newGame">New Game</button>
		</template>
	</div>
</template>

<script>
	import PokemonImage from "../components/PokemonImage.vue";
	import PokemonOptions from "../components/PokemonOptions.vue";
	import getPokemonOptions from "../helpers/getPokemonOptions";

	console.log(getPokemonOptions());

	export default {
		components: { PokemonImage, PokemonOptions },
		data() {
			return {
				pokemonArr: [],
				pokemon: null,
				showPokemon: false,
				showAnswer: false,
				message: "",
			};
		},
		methods: {
			async mixPokemonArray() {
				this.pokemonArr = await getPokemonOptions();
				const rndInt = Math.floor(Math.random() * 4);
				this.pokemon = this.pokemonArr[rndInt];
			},
			checkAnswer(pokemonId) {
				this.showPokemon = true;
				this.showAnswer = true;
				if (pokemonId === this.pokemon.id) {
					this.message = `Correcto, ${this.pokemon.name}`;
				} else {
					this.message = `Oops, era ${this.pokemon.name}`;
				}
			},
			newGame() {
				this.showAnswer = false;
				this.showPokemon = false;
				this.pokemon = null;
				this.pokemonArr = [];
				this.mixPokemonArray();
			},
		},
		mounted() {
			this.mixPokemonArray();
		},
	};
</script>

<style></style>
