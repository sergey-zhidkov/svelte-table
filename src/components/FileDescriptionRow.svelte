<script lang="ts">
	export let id: number
	export let fileDescription: FileDescription
	export let isSelected = false
	export let onChange: (id: number) => void
</script>

<div class="tr {isSelected ? 'selected' : '' }">
	<div class="td checkbox-container">
		<input type="checkbox" on:change={() => onChange(id)} checked={isSelected}/>
	</div>
	<div class="td name-container"><span>{fileDescription.name}</span></div>
	<div class="td device-container"><span>{fileDescription.device}</span></div>
	<div class="td path-container"><span>{fileDescription.path}</span></div>
	<div class="td status-container">
		<div class="status-icon {fileDescription.status}"></div><span class="status-label">{fileDescription.status}</span>
	</div>
</div>

<style>
	.tr {
		grid-template-areas:"cb na de pa st";
	}

	.checkbox-container {
		grid-area: cb;
		justify-content: center;
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

	.status-icon {
		height: 16px;
		width: 16px;
		border-radius: 50%;
		margin-inline-end: 8px;
	}

	.status-icon.available {
		background-color: green;
	}

	.status-icon.scheduled {
		background-color: darkorange;
	}

	.status-label {
		text-transform: capitalize;
	}

	.tr.selected {
		background-color: rgb(238, 238, 238);
	}

	.tr:hover {
		background-color: rgb(245, 245, 245);
	}

	@media screen and (max-width: 736px) {
		.tr {
			grid-template-areas:
			"cb sl do"
			"cb na pa"
			"cb de st";
			grid-template-columns: 2em 1fr 4fr;
		}

		.td {
			border-bottom: 1px dashed lightgrey;
			min-height: 2em;
		}
	}
</style>