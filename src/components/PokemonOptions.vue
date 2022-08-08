<template>
	<div class="options__container">
		<ul>
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
	}
	li {
		border: 1px solid black;
		border-radius: 5px;
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
		background-color: #eee;
	}
	.options__container {
		position: absolute;
		bottom: 0;
		width: 100%;
		padding: 30px;
		background-color: #eee;
		border-radius: 20px 20px 0 0;
	}
</style>
