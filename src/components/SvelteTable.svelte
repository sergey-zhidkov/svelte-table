<script lang="ts">
	import FileDescriptionRow from "./FileDescriptionRow.svelte"
	import TableHead from "./TableHead.svelte";

	export let data: FileDescription[] = []

	$: state = data.map(d=> ({
		isSelected: false,
		fileDescription: d,
	}))

	const handleOnChange = (id: number) => {
		const rowState = state[id]
		rowState.isSelected = !rowState.isSelected
		state = [...state]
	}
</script>

<div class="table-container">
	<TableHead selectedCount={state.filter(s => s.isSelected).length} totalCount={state.length} />
	<div class="tbody">
		{#each state as row, i}
			<FileDescriptionRow
				id={i}
				fileDescription={row.fileDescription}
				isSelected={row.isSelected}
				onChange={handleOnChange}
				/>
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