<template>
	<div class="options__container">
		<h2>Escoge tu</h2>
		<img src="/pokemonLogo.png" alt="" />
		<ul class="options">
			<li v-for="pokemon in pokemons" :key="pokemon.id">
				<a @click="$emit('selection', pokemon.id)">
					{{ pokemon.name }}
				</a>
			</li>
		</ul>
	</div>
</template>

<script>
	export default {
		props: {
			pokemons: {
				type: Array,
				required: true,
			},
		},
	};
</script>

<style scoped>
	ul {
		list-style: none;
		margin: 0%;
		padding: 0%;
		width: 100%;
	}
	li {
		border: 1px solid #215f98;
		border-radius: 5px;
		background-color: #2a75bb;
		color: #ffcb05;
		font-weight: 800;
		margin: 20px 0;
		text-transform: capitalize;
	}
	a {
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 10px;
	}
	a:active,
	a:hover {
		background-color: #ffcb05;
		color: #2a75bb;
	}
	.options__container {
		width: 100%;
	}
	.options__container img {
		width: 35%;
		margin-bottom: 10px;
	}
	.options__container h2 {
		margin: 0;
	}
	.options__container {
		height: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: space-between;
	}
	/* .options__container {
			position: absolute;
			bottom: 0;
			width: 100%;
			padding: 30px;
			background-color: #eee;
			border-radius: 20px 20px 0 0;
		} */
</style>
