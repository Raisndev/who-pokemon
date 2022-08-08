<template>
	<h1 v-if="!pokemon">Analizando Pokemones</h1>

	<template v-else>
		<div class="header__container">
			<h1>Que pokemon es?</h1>
			<PokemonImage :pokemonId="pokemon.id" :showPokemon="showPokemon" />
		</div>
		<div>
			<PokemonOptions
				v-if="!showAnswer"
				:pokemons="pokemonArr"
				@selection="checkAnswer($event)"
			/>
			<div class="answer" v-else>
				<h2>{{ message }}</h2>
				<button @click="newGame">New Game</button>
			</div>
		</div>
	</template>
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

<style>
	.answer {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 80%;
		border-radius: 20px;
		display: flex;
		flex-direction: column;
		gap: 10px;
		padding: 20px;
		background-color: rgb(156, 214, 156);
	}
	.answer h2 {
		margin: 0 0 10px 0;
	}
	.answer button {
		border: 0;
		padding: 10px;
		border-radius: 5px;
	}
</style>
