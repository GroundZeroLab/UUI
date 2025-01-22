<script lang="ts">
	import type { Size } from '$lib/index.js';
	import DropDown from '$lib/nav/DropDown.svelte';
	import Button from './Button.svelte';

	export let disabled: boolean = false;
	export let size: Size = 'md';
	export let items: string[] = [''];
	export let value: string = items[0];

	$: value = items[0];
</script>

<DropDown clickRequired border>
	<span slot="header" class="header {size}">{value}</span>
	<div slot="body" class="list">
		{#each items as item}
			<Button onClick={() => (value = item)} {size}>
				{item}
			</Button>
		{/each}
	</div>
</DropDown>

<select {disabled} bind:value />

<style>
	.sm {
		font-size: var(--font-size-sm);
	}
	.md {
		font-size: var(--font-size-md);
	}
	.lg {
		font-size: var(--font-size-lg);
	}

	select {
		-webkit-appearance: none;
		-moz-appearance: none;
		appearance: none;
		display: none;
		padding: 0.3rem 0.6rem;
		color: var(--text);
		border: none;
		cursor: pointer;
	}

	.list {
		display: grid;
		gap: 0.2rem;
		min-width: 100px;
		max-height: 150px;
		overflow-y: scroll;
	}

	.list :global(button) {
		text-align: left;
	}

	.list::-webkit-scrollbar {
		width: 6px;
	}

	.list::-webkit-scrollbar-track {
		background: #f1f1f1;
	}

	.list::-webkit-scrollbar-thumb {
		background: #888;
		border-radius: 4px;
	}

	.list::-webkit-scrollbar-thumb:hover {
		background: #555;
	}
	

</style>
