<script lang="ts">
	import { onMount } from 'svelte';

	export let show = false;
	let isMobile = false;

	onMount(() => {
		isMobile = window.innerWidth < 400;
	});
</script>

<button
	on:click={() => (show = !show)}
	on:mouseenter={() => (show = isMobile ? show : true)}
	on:mouseleave={() => (show = false)}
>
	<header>
		<slot name="header" />
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class:hovered={show}
			><path
				fill="none"
				stroke="currentColor"
				stroke-linecap="round"
				stroke-linejoin="round"
				stroke-width="48"
				d="M112 184l144 144 144-144"
			/></svg
		>
	</header>
	{#if show}
		<div class="body">
			<slot name="body" />
		</div>
	{/if}
</button>

<style>
	button {
		background-color: inherit;
		color: inherit;
		font-size: inherit;
		border: inherit;
		text-align: inherit;
		position: relative;
		padding: 0;
	}
	button svg.hovered {
		rotate: 180deg;
	}
	header {
		display: flex;
		align-items: end;
		gap: 0.2rem;
		cursor: pointer;
		font-size: var(--font-size-md);
		margin-bottom: 0.3rem;
		font-weight: bold;
	}
	svg {
		height: 14px;
		aspect-ratio: 1/1;
		display: block;
		transition: 0.2s;
	}
	.body {
		margin-left: -0.3rem;
		padding: 0.3rem;
		z-index: 1;
		position: absolute;
		backdrop-filter: blur(40px);
		-webkit-backdrop-filter: blur(40px);
		border-radius: 8px;
		border: 1px solid var(--border-color);
	}
</style>
