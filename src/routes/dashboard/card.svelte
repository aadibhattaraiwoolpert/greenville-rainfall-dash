<script>
	import RainIcon from './rain-icon.svelte';

	export let amount = 0.0;
	export let unit = 'in.';
	export let title = 'Rainfall 1-hr';
	export let cardColor = '#0064ff'; // Default color if not provided
</script>

<div class="card" style="background-color: {cardColor};">
	<div class="title">
		<span class="title-text"> {title}</span>
	</div>

	<div class="content">
		<div class="rain-amount">
			<div><RainIcon size="30"></RainIcon></div>
			<div class="amount-text">{amount} {unit}</div>
		</div>
	</div>
</div>

<style>
	.card {
		display: flex;
		flex-direction: column;

		flex: 1;
		margin: 0 0.5rem;
		padding: 1rem;

		/* background is now set dynamically */
		border-radius: 4px;
	}

	.title {
		border-bottom-color: #ccc;
		border-bottom-width: 1px;
		border-bottom-style: solid;
		padding: 0.3rem 0;
		margin-bottom: 1rem;
	}

	.title-text {
		font-size: 1rem;
		font-weight: 400;
	}

	.content {
		padding: 0.25rem 0rem;
	}

	.rain-amount {
		flex: 1;

		display: flex;
		flex-direction: row;
		justify-content: space-between;

		margin: 0 0.5rem;
		align-items: center;
		width: 100%;

		gap: 0.5rem;
	}

	.amount-text {
		font-size: 2rem;
		padding-right: 0.5rem;
	}
</style>