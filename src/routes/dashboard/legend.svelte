<script>
	// Example data for the legend
	const legendItems = [
		{ label: '0 - 2yr', color: '#00649a' },
		{ label: '2 - 5yr', color: '#00ff00' },
		{ label: '5 - 10yr', color: '#008000' },
		{ label: '10 - 25yr', color: '#ffff00' },
		{ label: '25 - 50yr', color: '#ffcc00' },
		{ label: '50 - 100yr', color: '#ff6600' },
		{ label: '100 - 500yr', color: '#ff0000' },
		{ label: '> 500yr', color: '#ff00ff' }
	];
</script>

<div class="legend-container">
	<div class="legend-title">Legend</div>
	<div class="legend-description">
		Tiles will change color when accumulated rainfall for the indicated time period falls within the
		following frequency ranges:
	</div>
	<div class="legend-items">
		{#each legendItems as item}
			<div class="legend-item" style="background-color: {item.color};">
				<div class="label">{item.label}</div>
			</div>
		{/each}
	</div>
</div>

<style>
	.legend-container {
		display: flex;
		flex-direction: column;
		background-color: #001f30;
		padding: 1rem;
		border-radius: 8px;
		color: #ccc;
		width: 75%;
		margin: auto;
	}

	.legend-title {
		font-size: 1.2rem;
		font-weight: bold;
		margin-bottom: 0.5rem;
		color: white;
	}

	.legend-description {
		font-size: 0.9rem;
		margin-bottom: 1rem;
		font-style: italic;
	}

	.legend-items {
		display: flex;
		justify-content: space-between;
		color: black;
	}

	.legend-item {
		display: flex;
		align-items: center;
		align-content: center;
		text-align: center;
		flex: 1;
		padding: 0.5rem;
		margin: 0 0.1rem;
		/* border: 1px solid #222; */
		border-radius: 4px;
	}

	.label {
		font-size: 1rem;
		width: 100%;
	}
</style>
