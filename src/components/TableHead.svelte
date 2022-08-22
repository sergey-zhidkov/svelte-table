<script lang="ts">
	export let selectedCount: number = 0
	export let totalCount: number

	$: selectedText = selectedCount === 0 ? "None Selected" : `Selected ${selectedCount}`
</script>

<div class="thead">
	<div class="tr">
		<div class="th indeterminate-checkbox-container"><intput type="checkbox" class="indeterminate-checkbox"/></div>
		<div class="th selected-label-container"><span>{selectedText}</span></div>
		<div class="th download-button-container"><button>Download Selected</button></div>
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
	.selected-label-container {
		grid-column: auto / span 2;
	}
	.download-button-container {
		grid-column: auto / span 2
	}
</style>