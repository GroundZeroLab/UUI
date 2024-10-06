<script lang="ts">
	import type { Size } from '$lib/index.js';

	export let size: Size = "md";
	export let group = '';
	export let checked = false;
	export let disabled = false;

	let sizeMapping = {
		sm: '0.4rem',
		md: '0.7rem',
		lg: '1rem'
	};
</script>

<label
	class:checked
	class:disabled
	on:click|stopPropagation={() => (checked = !checked)}
	class={size}
	style="--radio-size:{sizeMapping[size]}"
>
	<span />
	<slot />
</label>

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
