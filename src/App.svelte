<script lang="ts">
	import { fetchData } from "./utils/fetch-data";
	import SvelteTable from "./components/SvelteTable.svelte"

	let tableDataPromise = fetchData()
</script>

<main>
	{#await tableDataPromise}
		<div class="spinner">Loading...</div>
	{:then data}
		<SvelteTable data={data}/>
	{:catch error}
		<div class="error-message">{error}</div>
	{/await}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	.spinner {
		font-size: 40px;
		margin: 40px auto 40px auto;
	}

	.error-message {
		font-size: 40px;
		color: red;
		margin: 40px auto 40px auto;
	}
</style>