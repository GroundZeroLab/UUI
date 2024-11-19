<script lang="ts">
	import Card from '$lib/box/Card.svelte';
	import type { Size, Status } from '$lib/index.js';

	export let open = false;
	export let size: Size = 'sm';
	export let status: Status = undefined;

	function toggle() {
		open = !open;
	}
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<Card {size} {status}>
	<div class="title" on:click|stopPropagation={toggle} slot="header" class:open>
		<span class="chevron" class:open></span>
		<span><slot name="title" /></span>
	</div>
	{#if open}
		{#if $$slots.default}
			<slot />
		{/if}
		<!-- {#if $$slots.footer}
				<slot name="footer" slot="footer"/>
		{/if} -->
	{/if}
</Card>

<style>
	.title {
		cursor: pointer;
	}
	.chevron {
		display: inline-block;
		position: relative;
		bottom: 2px;
		border-left: 5px solid transparent;
		border-right: 5px solid transparent;
		border-top: 5px solid var(--pure);
		transition: transform 0.3s;
	}

	.chevron.open {
		transform: rotate(180deg);
	}
</style>
