<script lang="ts">
	import FileDescriptionRow from "./FileDescriptionRow.svelte"
	import TableHead from "./TableHead.svelte";

	export let data: FileDescription[] = []
	export let onDownloadClick: (selectedFiles: FileDescription[]) => void

	$: state = data.map(d=> ({
		isSelected: false,
		fileDescription: d,
	}))
	$: selectedCount = state.filter(s => s.isSelected).length

	const handleRowOnChange = (id: number) => {
		const rowState = state[id]
		rowState.isSelected = !rowState.isSelected
		state = [...state]
	}

	const handleSelectAllOnChange = (isChecked: boolean) => {
		if (isChecked) {
			state.forEach(s => s.isSelected = true)
		} else {
			state.forEach(s => s.isSelected = false)
		}
		state = [...state]
	}

	const handleOnDownloadClick = () => {
		const selectedFiles = state.filter(s => s.isSelected).map(s => s.fileDescription)
		onDownloadClick(selectedFiles)
	}
</script>

<div class="table-container">
	<TableHead
		selectedCount={selectedCount}
		totalCount={state.length}
		onChange={handleSelectAllOnChange}
		onDownloadClick={handleOnDownloadClick}
		/>
	<div class="tbody">
		{#each state as row, i}
			<FileDescriptionRow
				id={i}
				fileDescription={row.fileDescription}
				isSelected={row.isSelected}
				onChange={handleRowOnChange}
				/>
		{/each}
	</div>
</div>

<style>
	.table-container {
		box-shadow: 0px 0px 8px 0px rgba(0,0,0,0.35);
	}

	.thead {
	}

	:global(.table-container .tr) {
		display: grid;
		grid-template-columns: 2em 1fr 1fr 5fr 1fr;
		gap: 2px;
		min-height: 2.5em;
		background-color: white;
		border-bottom: 1px solid lightgray;
	}

	:global(.table-container .td), :global(.table-container .th) {
		/* border: 1px dashed black; */

		display: flex;
		align-items: center;
		justify-content: left;
	}

</style>