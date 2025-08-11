<script>
	import { onMount } from 'svelte';
	import Legend from './legend.svelte';
	import CardGroup from './card-group.svelte';

	const API_KEY = import.meta.env.VITE_API_KEY;
	const SHEET_ID = '19y0EK2ctJvwn4YTsY5KUCXySci6MYmErJ6Op1zz_izc'; //new spreadsheet
	const SHEET_RANGE = 'Rainfall Data!A1:P100'; //For 5 cards

	let data = [];

	onMount(async () => {
		try {
			await loadGapiScript();
			await initClient();
			data = await fetchSheetData();
		} catch (error) {
			console.error('Error fetching data:', error);
		}
	});

	function loadGapiScript() {
		return new Promise((resolve, reject) => {
			const script = document.createElement('script');
			script.src = 'https://apis.google.com/js/api.js';
			script.onload = () => resolve();
			script.onerror = () => reject('Failed to load gapi script');
			document.body.appendChild(script);
		});
	}

	function initClient() {
		return new Promise((resolve, reject) => {
			gapi.load('client', () => {
				gapi.client
					.init({
						apiKey: API_KEY,
						discoveryDocs: ['https://sheets.googleapis.com/$discovery/rest?version=v4']
					})
					.then(resolve, reject);
			});
		});
	}

	function transformData(rawData) {
		const headers = rawData[0];
		const rows = rawData.slice(1);
		return rows.map((row) => {
			let rowData = {};
			row.forEach((value, index) => {
				rowData[headers[index]] = value;
			});
			return rowData;
		});
	}

	async function fetchSheetData() {
		const data = await gapi.client.sheets.spreadsheets.values.get({
			spreadsheetId: SHEET_ID,
			range: SHEET_RANGE
		});

		const values = data.result.values;
		const transformedData = transformData(values);
		console.log('fetched', transformedData);
		return transformedData;
	}
</script>

<div class="container">
	<h1 class="title">Greenville County Rainfall Dashboard</h1>

	<Legend></Legend>

	<div class="cards">
		{#each data as row}
			<CardGroup data={row}></CardGroup>
		{/each}
	</div>
</div>

<style>
	.title {
		text-align: center;
		margin-bottom: 3rem;
	}

	.container {
		max-width: 1200px;
		margin: 0 auto;
		padding: 2rem;
	}

	.cards {
		margin-top: 3rem;
	}
</style>