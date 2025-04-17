<script lang="ts">
	import type { Status } from '$lib/index.js';

	export let id = '';
	export let name = '';
	export let value = '';
	export let placeholder = '';
	export let disabled = false;
	export let size = 'md';
	export let cols = 20;
	export let rows = 3;
	export let status: Status = undefined;
	export let hover = false;
	export let selected = false;

	function onInput(e: Event & { currentTarget: EventTarget & HTMLTextAreaElement }) {
		if (!e || !e.target) return;
		const target = e.target as HTMLTextAreaElement;
		value = target.value;
	}
</script>

<div class="border" style="--bd-color:{status ? `var(--${status})` : 'var(--border-color)'}" class:hover class:selected>
	<textarea
		{name}
		{id}
		{placeholder}
		{disabled}
		{rows}
		{cols}
		{value}
		class={size}

		on:input={onInput}
	></textarea>
</div>

<style>
	.sm {
		zoom: 0.8;
	}

	.md {
		zoom: 1;
	}

	.lg {
		zoom: 1.2;
	}
	.border {
		border: 1px solid var(--bd-color);
		border-radius: var(--border-radius);

	}

	.border.selected {
		border-color: var(--focus-color);
	}

	.border.hover:hover {
		border-color: var(--focus-color);
	}

	textarea {
		font-family:
			system-ui,
			-apple-system,
			BlinkMacSystemFont,
			'Segoe UI',
			Roboto,
			Oxygen,
			Ubuntu,
			Cantarell,
			'Open Sans',
			'Helvetica Neue',
			sans-serif;
		margin: 2px 2px 1px 2px;
		border: none;
		background-color: var(--bg-color);
		color: var(--text-color);
		font-size: var(--font-size-md);
		height: fit-content;
		min-height: 1rem;
		min-width: 5.2rem;
	}
	textarea:disabled {
		cursor: not-allowed;
		background-color: transparent;
		color: var(--text-color);
		opacity: 0.5;
	}

	textarea:active,
	textarea:focus {
		border-color: var(--primary-color);
		outline: none;
	}
</style>
