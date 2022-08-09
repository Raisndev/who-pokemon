<template>
	<img :src="answerImg" alt="" />
	<div class="answer">
		<h2>{{ message }}</h2>
		<span>{{ pkmName }}</span>
	</div>
	<button @click="$emit('newGame')">{{ btnText }}</button>
</template>

<script>
	export default {
		props: {
			message: {
				type: String,
				required: true,
			},
			pkmName: {
				type: String,
				required: true,
			},
			btnText: {
				type: String,
				required: true,
			},
			answerImg: {
				type: String,
				required: true,
			},
		},
	};
</script>

<style scoped>
	img {
		width: 70vw;
	}
	.answer h2 {
		margin: 0 0 10px 0;
	}
	.answer span {
		text-transform: capitalize;
		font-size: 30px;
		font-weight: 800;
		color: #ffcb05;
	}
	button {
		border: 0;
		padding: 15px;
		border-radius: 5px;
		font-size: 16px;
		margin-top: 30px;
		width: 70vw;
		border: 1px solid #215f98;
		border-radius: 5px;
		background-color: #2a75bb;
		color: #ffcb05;
		font-weight: 800;
		text-transform: uppercase;
	}
</style>
