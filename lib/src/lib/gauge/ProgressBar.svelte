<script lang="ts">
	export let value = 0;
	$: valuePourcent = Math.min(100, Math.max(0, value)) + '%';
</script>

<div class="bar">
	<div class="bar" style="--value:{valuePourcent}" />
</div>

<style>
	.bar {
		background-color: var(--border-color);
		height: 0.5rem;
		width: 100%;
		border-radius: var(--border-radius);
		transition: 0.3s;
	}

	.bar > .bar {
		background-color: var(--pure);
		height: 100%;
		width: var(--value);
	}
</style>
