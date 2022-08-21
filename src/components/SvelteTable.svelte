<script lang="ts">
	export let data: FileDescription[] = []
	console.log(data)
</script>

<main>
	<div class="table-container">
		<div class="thead">
			<div class="tr">
				<div class="th"><intput type="checkbox"/></div>
				<div class="th"><button>Download Selected</button></div>
			</div>
			<div class="tr">
				<div class="th"></div>
				<div class="th"><span>Name</span></div>
				<div class="th"><span>Device</span></div>
				<div class="th"><span>Path</span></div>
				<div class="th"><span>Status</span></div>
			</div>
		</div>
		<div class="tbody">
			{#each data as row (row.path)}
				<div class="tr">
					<div class="td"><input type="checkbox"/></div>
					<div class="td"><span>{row.name}</span></div>
					<div class="td"><span>{row.device}</span></div>
					<div class="td"><span>{row.path}</span></div>
					<div class="td"><div class="status-icon"></div><span>{row.status}</span></div>
				</div>
			{/each}
		</div>
	</div>
	<h1>{data}</h1>
</main>

<style>

</style>