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
			<img src="/favicon.png" class="download-icon" alt="download files icon"/>
			<button class="download-button" disabled={selectedCount === 0} on:click={onDownloadClick}>Download Selected</button>
		</div>
	</div>
	<div class="tr">
		<div class="th"></div>
		<div class="th name-container"><span>Name</span></div>
		<div class="th device-container"><span>Device</span></div>
		<div class="th path-container"><span>Path</span></div>
		<div class="th status-container"><span>Status</span></div>
	</div>
</div>

<style>

	.tr {
		grid-template-areas:
		"cb sl sl do do"
		".  na de pa st";
	}
	.indeterminate-checkbox-container {
		justify-content: center;
		align-items: center;
		grid-area: cb;
	}

	.selected-label-container {
		grid-area: sl;
	}
	.download-button-container {
		display: flex;
		align-items: center;
		grid-area: do;
	}

	.name-container {
		grid-area: na;
	}

	.device-container {
		grid-area: de;
	}

	.path-container {
		grid-area: pa;
	}

	.status-container {
		grid-area: st;
	}

	/* Placeholder for real icon */
	/* TOOD: find a better icon */
	.download-icon {
		margin-inline-end: 8px;
		height: 16px;
		width: 16px;
	}

	.download-button:hover:enabled {
		background-color: lightskyblue;
		cursor: pointer;
	}

	.download-button {
		border: none;
		min-height: 2em;
	}

	@media screen and (max-width: 736px) {
		.tr {
			grid-template-areas:
			"cb sl do"
			". na pa"
			". de st";
			grid-template-columns: 2em 1fr 4fr;
		}
	}
</style>