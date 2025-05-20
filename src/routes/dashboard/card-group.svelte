<script>
	export let data;

	import Card from './card.svelte';
</script>

{#if data}
	<div class="card-container">
		<h1 class="card-title">{data.SiteName}</h1>

		<div class="cards">
			<Card amount={data.Rainfall_1h} title="Rainfall 1-hr" cardColor={data.Rainfall_1h_Color}></Card>
			<Card amount={data.Rainfall_3h} title="Rainfall 3-hr" cardColor={data.Rainfall_3h_Color}></Card>
			<Card amount={data.Rainfall_6h} title="Rainfall 6-hr" cardColor={data.Rainfall_6h_Color}></Card>
			<Card amount={data.Rainfall_12h} title="Rainfall 12-hr" cardColor={data.Rainfall_12h_Color}></Card>
			<Card amount={data.Rainfall_24h} title="Rainfall 24-hr" cardColor={data.Rainfal_24h_Color}></Card>
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