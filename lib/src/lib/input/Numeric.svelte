<script lang="ts">
	import type { Size } from '$lib/index.js';
	import Button from './Button.svelte';

	export let name: string = '';

	export let value: number | null = 0;
	export let min: number = 0;
	export let max: number = 100;
	export let step: number = 1;
	export let disabled: boolean = false;
	export let size: Size = 'md';

	function onChange(d: boolean) {
		if (disabled || value === null) return null;
		if (d) value = value + step;
		else value = value - step;
	}

	function check(value: number | null) {
		if (disabled || value === null) return null;
		if (value < min) value = min;
		if (value > max) value = max;
		return value;
	}

	$: value = check(value);

	$: width = max.toString().length * 0.68 + 'rem';
</script>

<div class="input">
	<input type="number" bind:value class={size} {disabled} style="--width:{width}" {name} />
	<div class="arrows">
		<Button onClick={() => onChange(true)} {disabled} {size} type="icon">&#9650;</Button>
		<Button onClick={() => onChange(false)} {disabled} {size} type="icon">&#9660;</Button>
	</div>
	<div class:disabled />
</div>

<style>
	.sm {
		height: 0.8rem;
		font-size: 14px;
		font-size: var(--font-size-sm);
		padding: 0.1rem 0rem 0.1rem 0.15rem;
	}
	.md {
		height: 1rem;
		font-size: var(--font-size-md);
		padding: 0.1rem 0rem 0.1rem 0.2rem;
	}
	.lg {
		height: 1.2rem;
		font-size: var(--font-size-lg);
		padding: 0.15rem 0rem 0.2rem 0.4rem;
	}

	input::-webkit-outer-spin-button,
	input::-webkit-inner-spin-button,
	input[type='number'] {
		-webkit-appearance: none;
		-moz-appearance: textfield;
		margin: 0;
	}

	input {
		width: var(--width);
		border: none;
		border-right: 1px solid var(--border-color);
		background-color: var(--bg-color);
		color: var(--text-color);
	}

	input:active,
	input:focus {
		border-color: var(--primary-color);
		outline: none;
	}

	.input {
		position: relative;
		overflow: hidden;
		display: flex;
		align-items: center;
		border: 1px solid var(--border-color);
		border-radius: var(--border-radius);
		height: fit-content;
		gap: 0.1rem;
	}

	.disabled {
		top: 0;
		position: absolute;
		height: 100%;
		width: 100%;
		z-index: 1;
		cursor: not-allowed;
	}

	.arrows {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}
</style>
