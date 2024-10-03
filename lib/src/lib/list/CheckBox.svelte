<script lang="ts">
	import type { Size } from '$lib/index.js';

	export let size: Size = undefined;
	export let group = '';
	export let checked = false;
	export let disabled = false;
</script>

<label class:checked class:disabled on:click|stopPropagation={() => (checked = !checked)}>
	<span />
	<slot />
</label>

<style>
	label.checked > span {
		background-color: var(--primary-color);
	}

	span {
		display: inline-block;
		width: 1rem;
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
