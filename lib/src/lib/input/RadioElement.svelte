<script lang="ts">
	import type { Size } from '$lib/index.js';

	export let size: Size = 'md';

	export let value = '';
	export let group: string = '';
	export let checked = false;
	export let disabled = false;
	export let id = group + Math.round(Math.random() * 1000);

	let sizeMapping = {
		sm: '0.4rem',
		md: '0.7rem',
		lg: '1rem'
	};
</script>

<label for={id} class={size} class:disabled style="--radio-size:{sizeMapping[size || "md"]}">
	<input type="radio" name={group} {id} bind:value {disabled} {checked} />
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

	/* label {
		display: flex;
		align-items: center;
		gap: 0.4rem;
		color: var(--pure);
	}

  label.disabled {
		cursor: not-allowed;
		background-color: transparent;
		color: var(--text-color);
		opacity: 0.6;
	} */

	input {
		position: absolute;
		opacity: 0;
		width: 0;
		height: 0;
	}
	span {
		width: var(--radio-size);
		aspect-ratio: 1/1;
		border-radius: 50%;
		border: 1px solid var(--border-color);
		background-color: var(--pure);
	}

	label.disabled {
		opacity: 0.5;
		cursor: not-allowed;
	}

	label {
		display: flex;
		align-items: center;
		cursor: pointer;
		gap: 0.4rem;
	}

	label:not(.disabled):hover span {
    background-color: var(--primary-color);

	}

	label > input:checked + span {
    background-color: var(--primary-color);
	}
</style>
