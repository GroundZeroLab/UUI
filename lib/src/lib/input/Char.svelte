<script lang="ts">
	import type { Size } from '$lib/index.js';
	import Button from './Button.svelte';

	export let value: string | null = 'A';
	export let min: string = 'A';
	export let max: string = 'ZZZ';

	let internalValue = 0;
	let minInternal = charToNumber(min);
	let maxInternal = charToNumber(max);

	export let disabled: boolean = false;
	export let size: Size = 'md';

	function numberToChar(n: number) {
		let result = '';
		while (n >= 0) {
			result = String.fromCharCode((n % 26) + 65) + result;
			n = Math.floor(n / 26) - 1;
		}
		return result;
	}

	function charToNumber(c: string) {
		let result = 0;
		for (let i = 0; i < c.length; i++) {
			result = result * 26 + c.charCodeAt(i) - 65;
		}
		return result;
	}

	function onChange(d: boolean) {
		if (disabled || value === null) return null;
		if (d) internalValue++;
		else internalValue--;
		value = numberToChar(internalValue);
	}

	function check(value: string | null) {
		if (disabled || value === null) return null;
		if (internalValue <= minInternal) internalValue = minInternal;
		if (internalValue >= maxInternal) internalValue = maxInternal;
		const nValue= numberToChar(internalValue);
		if(nValue !== value) return nValue;
		return value.toUpperCase();
	}

	$: value = check(value);
	$: width = max.toString().length * 0.75 + 'rem';
</script>

<div class="input">
	<input type="text" bind:value class={size} {disabled} style="--width:{width}" />
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
		padding: 0.1rem 0.1rem 0.2rem 0.3rem;
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
		border-radius: 0.2rem;
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
