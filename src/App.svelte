<script lang="ts">
	import { fetchData } from "./utils/fetch-data";
	import SvelteTable from "./components/SvelteTable.svelte"

	let tableDataPromise = fetchData()

	const handleOnDownloadClick = (selectedFiles: FileDescription[]) => {
		// Trigger download for available files
		const availableFiles = selectedFiles.filter(f => f.status === "available")
		const unavailableFiles = selectedFiles.filter(f => f.status !== "available")

		let message = ""
		if (availableFiles.length) {
			message +=
			`Downloading files:\n ${availableFiles.map(f => `Device: ${f.device}; Path: ${f.path};\n`)}\n`
		}
		if (unavailableFiles.length) {
			message +=
			`Files are not available:\n ${unavailableFiles.map(f => `Device: ${f.device}; Path: ${f.path}; Status: ${f.status};\n`)}\n`
		}
		// Can download message
		alert(message)
	}
</script>

<main>
	{#await tableDataPromise}
		<div class="spinner">Loading...</div>
	{:then data}
		<SvelteTable data={data} onDownloadClick={handleOnDownloadClick}/>
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