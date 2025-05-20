<script>
    // Example data for the legend
    const legendItems = [
        { label: '<1 yr', color: '#00649a' }, // Light Blue
        { label: '1 yr', color: '#A99BBE' },  // Light Purple
        { label: '2 yr', color: '#8067A1' },  // Medium Purple
        { label: '5 yr', color: '#A64D79' },  // Darker Purple/Red
        { label: '10 yr', color: '#D94A4A' }, // Bright Red
        { label: '25 yr', color: '#F0742B' }, // Red-Orange
        { label: '50 yr', color: '#F7A827' }, // Orange
        { label: '100 yr', color: '#F7C52B' },// Yellow-Orange
        { label: '200 yr', color: '#F7E22B' },// Yellow
        { label: '500 yr', color: '#FFFF7F' },// Light Yellow
        { label: '1000 yr', color: '#FFFFBF'} // Very Light Yellow
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
