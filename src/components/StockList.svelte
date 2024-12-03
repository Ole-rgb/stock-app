<script>
    import { onMount } from 'svelte';

    let stocks = [];
    export let api_base_url;

   export async function fetchStocks(){
        const response = await fetch(`${api_base_url}/stocks/`);
        if(response.ok){
            const data = await response.json();
            stocks = data.tickers || [];
        }else{
            console.error('Failed to fetch stocks');
        }
    }

    onMount(async () => {
        fetchStocks();
    });
</script>

<style>
    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        padding: 8px;
        border-bottom: 1px solid #ccc;
    }
</style>

<h1>Stock Observation List</h1>
<ul>
    {#each stocks as stock}
        <li>{stock}</li> <!-- Display the stock ticker -->
    {/each}
</ul>

