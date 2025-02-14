<script lang="ts">
	import type { Size } from '$lib/index.js';
	import Button from '$lib/input/Button.svelte';

	export let size: Size = 'md';
	export let checked = false;
	export let disabled = false;
</script>

<Button type="icon" onClick={() => (checked = !checked)}>
	<label class:checked class:disabled class={size}>
		<span></span>
		<slot />
	</label>
</Button>

<style>
	.sm {
		font-size: var(--font-size-sm);
		--radio-size: 0.4rem;
	}
	.md {
		font-size: var(--font-size-md);
		--radio-size: 0.7rem;
	}
	.lg {
		font-size: var(--font-size-lg);
		--radio-size: 1rem;
	}

	label.checked > span {
		background-color: var(--primary-color);
	}

	span {
		display: inline-block;
		width: var(--radio-size);
		aspect-ratio: 1/1;
		border-radius: 50%;
		border: 1px solid var(--border-color);
		margin-right: 5px;
	}

	label.disabled {
		opacity: 0.5;
		cursor: not-allowed;
	}

	label {
		display: inline-flex;
		align-items: center;
		cursor: pointer;
		height: fit-content;
	}
</style>
