<script>
    import StockList from '../components/StockList.svelte';
    import AddStockForm from '../components/AddStockForm.svelte';
    import { PUBLIC_API_BASE_URL } from '$env/static/public';
	
    let StockListComponent;
    function handleStockAdded(event) {
        if(StockListComponent){
            // Fetch the stocks again to update the list
            StockListComponent.fetchStocks();
        }
    }
</script>

<style>
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
</style>

<h1>Hello!</h1>
<AddStockForm api_base_url={PUBLIC_API_BASE_URL} on:stockAdded={handleStockAdded}/>
<StockList bind:this={StockListComponent} api_base_url={PUBLIC_API_BASE_URL}/>

