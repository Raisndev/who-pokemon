<template>
	<div class="using__desktop" v-if="isDesktop">
		<img src="/gifs/bad.gif" alt="" />
		<h2>Sorry, you're using a Desktop, this app only works on mobile</h2>
	</div>
	<template v-else>
		<h1 v-if="!pokemon">Analizando Pokemones</h1>

		<template v-else>
			<div class="header__container">
				<!-- <h2>Hello Da</h2> -->
				<img src="../assets/whosthatlogo.png" alt="Who's that Pokemon Logo" />
				<PokemonImage :pokemonId="pokemon.id" :showPokemon="showPokemon" />
			</div>
			<div class="functionality">
				<PokemonOptions
					v-if="!showAnswer"
					:pokemons="pokemonArr"
					@selection="checkAnswer($event)"
				/>
				<PokemonAnswer
					v-else
					:message="message"
					:btnText="btnText"
					:pkmName="pkmName"
					:answerImg="answerImg"
					@newGame="newGame()"
				/>
			</div>
		</template>
	</template>
</template>

<script>
	import PokemonImage from "../components/PokemonImage.vue";
	import PokemonOptions from "../components/PokemonOptions.vue";
	import PokemonAnswer from "../components/PokemonAnswer.vue";
	import getPokemonOptions from "../helpers/getPokemonOptions";

	console.log(getPokemonOptions());

	export default {
		components: { PokemonImage, PokemonOptions, PokemonAnswer },
		data() {
			return {
				pokemonArr: [],
				pokemon: null,
				showPokemon: false,
				showAnswer: false,
				message: "",
				btnText: "",
				answerImg: "",
				pkmName: "",
				isDesktop: false,
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
				this.pkmName = `${this.pokemon.name}`;
				if (pokemonId === this.pokemon.id) {
					this.message = `Correcto, és`;
					this.btnText = "Siguiente";
					this.answerImg = "/gifs/good.gif";
				} else {
					this.message = `Oops, era`;
					this.btnText = "New Game";
					this.answerImg = "/gifs/bad.gif";
				}
			},
			newGame() {
				this.showAnswer = false;
				this.showPokemon = false;
				this.pokemon = null;
				this.pokemonArr = [];
				this.mixPokemonArray();
			},
			checkDesktop() {
				let details = navigator.userAgent;
				let regexp = /android|iphone|kindle|ipad/i;
				let isMobileDevice = regexp.test(details);

				if (!isMobileDevice) {
					console.log("You are using a Desktop");
					this.isDesktop = true;
				}
			},
			calculateVh() {
				var vh = window.innerHeight;
				console.log(vh);
				document.documentElement.style.setProperty("--vh", vh + "px");
			},
		},
		created() {
			this.checkDesktop();
		},
		mounted() {
			// Initial calculation
			this.calculateVh();

			// Re-calculate on resize
			window.addEventListener("resize", this.calculateVh);

			// Re-calculate on device orientation change
			window.addEventListener("orientationchange", this.calculateVh);
			this.mixPokemonArray();
		},
	};
</script>

<style>
	h2,
	h1 {
		color: #ffcb05;
	}
	.using__desktop {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100%;
		padding: 10px;
	}
	.header__container {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 20px;
		margin: 25px;
	}
	.header__container img {
		width: 50vw;
	}
	.functionality {
		width: 100%;
		height: 50vh;
		padding: 20px 30px;
		background-color: rgb(23 40 62);
		border-radius: 10px 10px 0 0;
		display: flex;
		justify-content: flex-end;
		flex-direction: column;
		align-items: center;
	}
</style>
