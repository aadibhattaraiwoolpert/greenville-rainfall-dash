<script>
    import { onMount } from 'svelte';
    import Legend from './legend.svelte';
    import CardGroup from './card-group.svelte';

    const API_KEY = import.meta.env.VITE_API_KEY;
    const SHEET_ID = '1r4C0aDzq21_Nl9szpqd_TweC2785EY98Jt8GaOC0am4';
    const SHEET_RANGE = 'Rainfall Data!A1:I100'; // Adjusted range to include color data

    let data = [];
    let loading = true;

    onMount(async () => {
        try {
            await loadGapiScript();
            await initClient();
            data = await fetchSheetData();
        } catch (error) {
            console.error('Error fetching data:', error);
        } finally {
            loading = false;
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
        if (!rawData || rawData.length === 0) {
            return [];
        }
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
        try {
            const response = await gapi.client.sheets.spreadsheets.values.get({
                spreadsheetId: SHEET_ID,
                range: SHEET_RANGE
            });

            const values = response.result.values;
            const transformedData = transformData(values);
            console.log('fetched', transformedData);
            return transformedData;
        } catch (error) {
            console.error('Error fetching sheet data: ', error);
            throw error;
        }
    }
</script>

<div class="container">
    <h1 class="title">Columbia's Rainfall Dashboard</h1>

    <Legend></Legend>

    <div class="cards">
        {#if loading}
            <p>Loading data...</p>
        {:else if data.length > 0}
            {#each data as row}
                <CardGroup
                    data={{
                        SiteName: row.SiteName,
                        Rainfall_1h: row.Rainfall_1h,
                        Rainfall_3h: row.Rainfall_3h,
                        Rainfall_6h: row.Rainfall_6h,
                        Rainfall_12h: row.Rainfall_12h,
                        Rainfall_1h_color: row.Rainfall_1h_color,
                        Rainfall_3h_color: row.Rainfall_3h_color,
                        Rainfall_6h_color: row.Rainfall_6h_color,
                        Rainfall_12h_color: row.Rainfall_12h_color,
                    }}
                ></CardGroup>
            {/each}
        {:else}
            <p>No data available.</p>
        {/if}
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