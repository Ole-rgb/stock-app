<script>
    import { createEventDispatcher } from 'svelte';
    
    const dispatch = createEventDispatcher();
    
    let ticker = '';
    let startDate = '';
    let endDate = '';

    export let api_base_url;
    
    async function addStock() {
        const response = await fetch(`${api_base_url}/stocks/`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                ticker,
                start_date: startDate,
                end_date: endDate
            })
        });

        if (response.ok) {
            const data = await response.json();
            dispatch('stockAdded', data);
            ticker = '';
            startDate = '';
            endDate = '';
            console.log('Stock added: ', data.ticker);
        } else {
            console.error('Failed to add stock');
        }
    }
</script>

<style>
    form {
        display: flex;
        flex-direction: column;
        gap: 10px;
    }

    input {
        padding: 8px;
        font-size: 1em;
    }

    button {
        padding: 10px;
        background-color: #ff3e00;
        color: white;
        border: none;
        cursor: pointer;
    }

    button:hover {
        background-color: #e63600;
    }
</style>

<form on:submit|preventDefault={addStock}>
    <input type="text" placeholder="Ticker" bind:value={ticker} required />
    <input type="date" placeholder="Start Date" bind:value={startDate} required />
    <input type="date" placeholder="End Date" bind:value={endDate} required />
    <button type="submit">Add Stock</button>
</form>