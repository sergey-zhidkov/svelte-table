<script lang="ts">
	import FileDescriptionRow from "./FileDescriptionRow.svelte"
	import TableHead from "./TableHead.svelte";

	export let data: FileDescription[] = []

	// $: state = data.
	console.log(data)
</script>

<div class="table-container">
	<TableHead selected={1} />
	<div class="tbody">
		{#each data as row (row.path)}
			<FileDescriptionRow fileDescription={row} isSelected />
		{/each}
	</div>
</div>

<style>
	.table-container {
	}

	.thead {

	}

	:global(.table-container .tr) {
		display: grid;
		grid-template-columns: 2em 1fr 1fr 5fr 1fr;
		gap: 2px;
		min-height: 2.5em;
		background-color: white;
	}

	:global(.table-container .td), :global(.table-container .th) {
		border: 1px dashed black;

		display: flex;
		align-items: center;
		justify-content: left;
	}

</style>