<script lang="ts">
	export let fileDescription: FileDescription
	export let isSelected = false
</script>

<div class={"tr"}>
	<div class="td checkbox-container"><input type="checkbox"/></div>
	<div class="td"><span>{fileDescription.name}</span></div>
	<div class="td"><span>{fileDescription.device}</span></div>
	<div class="td"><span>{fileDescription.path}</span></div>
	<div class="td">
		<div class="status-container">
			<div class="status-icon {fileDescription.status}"></div><span class="status-label">{fileDescription.status}</span>
		</div>
	</div>
</div>

<style>
	.checkbox-container {
		justify-content: center;
	}

	.status-container {
		display: flex;
		align-items: center;
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

	.tr:hover {
		background-color: rgb(245, 245, 245);
	}
	.tr.selected {
		background-color: rgb(245, 245, 245);
	}
</style>