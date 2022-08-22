<script lang="ts">
	import { onMount } from 'svelte';

	export let selectedCount: number = 0
	export let totalCount: number
	export let onChange: (checked: boolean) => void

	let indeterminateCheckbox: HTMLInputElement | undefined

	const setInterminateStatus = (isIndeterminate: boolean, isChecked: boolean) => {
		if (!indeterminateCheckbox) {
			return
		}
		indeterminateCheckbox.indeterminate = isIndeterminate
		indeterminateCheckbox.checked = isChecked
	}

	$: selectedText = selectedCount === 0 ? "None Selected" : `Selected ${selectedCount}`
	$: isIndeterminate = selectedCount !== 0 && selectedCount < totalCount
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
				on:change={e => onChange(e.target.checked)}
				/>
		</div>
		<div class="th selected-label-container"><span>{selectedText}</span></div>
		<div class="th download-button-container">
			<div>icon</div>
			<button class="download-button">Download Selected</button>
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

	.indeterminate-checkbox {
		margin: 0;
	}

	.selected-label-container {
		grid-column: auto / span 2;
	}
	.download-button-container {
		grid-column: auto / span 2
	}
</style>