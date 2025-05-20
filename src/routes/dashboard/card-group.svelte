<script>
	export let data;

	import rainIcon from '$lib/assets/rain.svg?raw';
	import Card from './card.svelte';
	import RainIcon from './rain-icon.svelte';
</script>

{#if data}
	<div class="card-container">
		<h1 class="card-title">{data.SiteName}</h1>

		<div class="cards">
			<Card amount={data.Rainfall_1h} title="Rainfall 1-hr" colorHex={data.Rainfall_1h_color}></Card>
			<Card amount={data.Rainfall_3h} title="Rainfall 3-hr" colorHex={data.Rainfall_3h_color}></Card>
			<Card amount={data.Rainfall_6h} title="Rainfall 6-hr" colorHex={data.Rainfall_6h_color}></Card>
			<Card amount={data.Rainfall_12h} title="Rainfall 12-hr" colorHex={data.Rainfall_12h_color}></Card>
		</div>
	</div>
{/if}

<style>
	.card-container {
		/* background-color: #171717; */
		border-radius: 8px;
		padding: 0.5rem;
		margin-bottom: 1.5rem;
	}

	.card-title {
		color: #fff;
		font-weight: 900;
		font-size: 1.75rem;
		margin-left: 0.5rem;
	}

	.cards {
		display: flex;
		flex-direction: row;
	}
</style>