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

<DropDown clickRequired>
	<span slot="header">{value}</span>
	<div slot="body" class="list">
		{#each items as item}
			<Button onClick={() => (value = item)}>
				{item}
			</Button>
		{/each}
	</div>
</DropDown>

<select class={size} {disabled} bind:value />

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

	select:disabled {
		background-color: var(--bg-color-disabled);
		color: var(--text-disabled);
		cursor: not-allowed;
		opacity: 0.5;
	}

	.list {
		display: grid;
		gap: 0.2rem;
		min-width: 100px;
		max-height: 250px;
		overflow: scroll;
	}
</style>
