<script lang="ts">
	import type { Size } from '$lib/index.js';
	import CheckBox from './CheckBox.svelte';

	export let checkbox = false;
	export let checked = false;
	export let parentChecked = false;

	$: checked = parentChecked;

	export let size: Size = undefined;
</script>

<li class={size}>
	<div class="title">
		{#if checkbox}
			<CheckBox bind:checked></CheckBox>
		{/if}
		<h3>
			<slot name="title" />
		</h3>
		<span>
			<slot name="at" />
		</span>
	</div>
	{#if $$slots.subtitle}
		<div class="subtitle">
			<slot name="subtitle" />
		</div>
	{/if}
	{#if $$slots.content}
		<div class="content">
			<slot name="content" />
		</div>
	{/if}
</li>

<style>
	.sm {
		width: 300px;
	}

	.md {
		width: 400px;
	}

	.lg {
		width: 500px;
	}

	li {
		transition: 0.3s;
		padding: 0.5rem 0;
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
		min-width: 100px;
		transition: 0.3s;
	}
	.title {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 0.1rem;
	}

	.title h3 {
		color: var(--text-color);
		margin: 0;
		flex: 1;
	}

	.title span {
		color: var(--text-color-light);
	}

	.subtitle {
		color: var(--text-color-light);
	}

	.content {
		color: var(--text-color-lighter);
	}
</style>
