<script lang="ts">
	import type { Size, Status } from '$lib/index.js';
	import Button from './Button.svelte';

	export let disabled: boolean = false;
	export let size: Size = 'md';
	export let status: Status = undefined;
	export let maxLength: number = 3;

	export let onChange;

	const OFFSET = {
		sm: 0.6,
		md: 0.73,
		lg: 0.8
	};

	const currentOffset = OFFSET[size || 'md'];

	$: width = maxLength * currentOffset + 'rem';
</script>

<div
	class="input {size}"
	style="--bd-color:{status ? `var(--${status})` : 'var(--border-color)'}; --width:{width}"
>
	<slot />
	<div class="arrows">
		<Button onClick={() => onChange(true)} {disabled} {size} type="icon">&#9650;</Button>
		<Button onClick={() => onChange(false)} {disabled} {size} type="icon">&#9660;</Button>
	</div>
	<div class:disabled />
</div>

<style>
	.input :global(input::-webkit-outer-spin-button),
	.input :global(input::-webkit-inner-spin-button),
	.input :global(input) {
		-webkit-appearance: none;
		-moz-appearance: none;
		appearance: none;
		margin: 0;
	}

	.input :global(input) {
		width: var(--width);
		border: none;
		border-right: 1px solid var(--border-color);
		background-color: var(--bg-color);
		color: var(--text-color);
		padding: 0 0.2rem;
	}

	.sm :global(input) {
		height: 0.8rem;
		font-size: 14px;
		font-size: var(--font-size-sm);
		padding: 0.1rem 0.1rem 0.1rem 0.15rem;
	}
	.md :global(input) {
		height: 1rem;
		font-size: var(--font-size-md);
		padding: 0.1rem 0.1rem 0.1rem 0.2rem;
	}
	.lg :global(input) {
		height: 1.2rem;
		font-size: var(--font-size-lg);
		padding: 0.15rem 0.1rem 0.2rem 0.4rem;
	}

	.input :global(input:active),
	.input :global(input:focus) {
		border-color: var(--primary-color);
		outline: none;
	}

	.input {
		position: relative;
		overflow: hidden;
		display: flex;
		align-items: center;
		border: 1px solid var(--bd-color);
		border-radius: var(--border-radius);
		gap: 0.1rem;
		padding: 0.05rem;
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
		max-height: 1.8rem;
		margin: 0 1px;
		display: flex;
		flex-direction: column;
		-webkit-user-select: none; /* Safari */
		-ms-user-select: none; /* IE 10 and IE 11 */
		user-select: none; /* Standard syntax */
	}
</style>
