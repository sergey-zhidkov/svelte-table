<script lang="ts">
	import { onMount } from 'svelte';

	export let selectedCount: number = 0
	export let totalCount: number
	export let onChange: (checked: boolean) => void
	export let onDownloadClick: () => void

	let indeterminateCheckbox: HTMLInputElement | undefined

	const setInterminateStatus = (isIndeterminate: boolean, isChecked: boolean) => {
		if (!indeterminateCheckbox) {
			return
		}
		indeterminateCheckbox.indeterminate = isIndeterminate
		indeterminateCheckbox.checked = isChecked
	}

	const handleOnChange = (e: Event) => {
		onChange((e.target as HTMLInputElement).checked)
	}

	$: selectedText = selectedCount === 0 ? "None Selected" : `Selected ${selectedCount}`
	$: isIndeterminate = selectedCount !== 0 && selectedCount < totalCount;
	$: isChecked = selectedCount === totalCount
	$: setInterminateStatus(isIndeterminate, isChecked)
	onMount(() => setInterminateStatus(isIndeterminate, isChecked))
</script>

<div class="thead">
	<div class="tr">
		<div class="th indeterminate-checkbox-container">
			<input
				type="checkbox"
				class="indeterminate-checkbox"
				bind:this={indeterminateCheckbox}
				on:change={handleOnChange}
				/>
		</div>
		<div class="th selected-label-container"><span>{selectedText}</span></div>
		<div class="th download-button-container">
			<div class="download-icon">icon</div>
			<button class="download-button" disabled={selectedCount === 0} on:click={onDownloadClick}>Download Selected</button>
		</div>
	</div>
	<div class="tr">
		<div class="th"></div>
		<div class="th"><span>Name</span></div>
		<div class="th"><span>Device</span></div>
		<div class="th"><span>Path</span></div>
		<div class="th"><span>Status</span></div>
	</div>
</div>

<style>
	.indeterminate-checkbox-container {
		justify-content: center;
		align-items: center;
	}

	.selected-label-container {
		grid-column: auto / span 2;
	}
	.download-button-container {
		grid-column: auto / span 2


	}

	/* Placeholder for real icon */
	.download-icon {
		margin-inline-end: 8px;
		/* height: 16px; */
		/* width: 16px; */
	}
</style>