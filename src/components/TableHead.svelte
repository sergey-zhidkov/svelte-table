<script lang="ts">
	export let selected: number = 0

	$: selectedText = selected === 0 ? "None Selected" : `Selected ${selected}`
</script>

<div class="thead">
	<div class="tr">
		<div class="th"><intput type="checkbox"/></div>
		<div class="th selected-label"><span>{selectedText}</span></div>
		<div class="th download-button"><button>Download Selected</button></div>
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
	.selected-label {
		grid-column: auto / span 2;
	}
	.download-button {
		grid-column: auto / span 2
	}
</style>