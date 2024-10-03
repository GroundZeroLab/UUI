<script lang="ts">
	import type { Size } from '$lib/index.js';

	export let action: 'button' | 'submit' | 'reset' = 'button';
	export let type: 'danger' | 'warning' | 'info' | 'success' | '' = '';
	export let primary: boolean = false;
	export let disabled: boolean = false;

	export let size: Size = 'md';
	export let onClick: () => void = () => {};
</script>

<button type={action} class:typed={type} class:primary class:disabled class="{size} {type}"
on:click={disabled ? undefined : onClick}
>
	<slot />
</button>

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

	:global(:root) {
		--button-bg-color: rgb(31, 111, 235);
		--button-bg-color-hover: rgb(22, 94, 255);
		--button-text-color: #ffffff;
	}

	button {
		background-color: var(--primary-bg-color);
		border: 1px solid var(--border-color);
		font-weight: bold;
		font-size: var(--font-size-md);
		height: fit-content;
		padding: 0.4rem 0.8rem;
		border-radius: 0.5rem;
		cursor: pointer;
		transition: 0.2s;
		color: var(--pure);
	}
	button:hover {
		background-color: var(--button-bg-color);
		color: var(--button-text-color);
	}

	button.primary {
		background-color: var(--button-bg-color);
		color: var(--button-text-color);
	}

	button.primary:hover:not(.disabled) {
		background-color: var(--button-bg-color-hover);
	}
	button.disabled {
		cursor: not-allowed;
		background-color: transparent;
		color: var(--text-color);
		opacity: 0.6;
	}

	.typed{
		color: var(--bg-color);
	}

	.typed:hover:not(.disabled) {
		color: var(--border-color);
	}

	.danger {
		background-color: var(--danger);
	}
	.danger:hover:not(.disabled) {
		background-color: var(--danger-light);
	}

	.warning {
		background-color: var(--warning);
	}
	.warning:hover:not(.disabled) {
		background-color: var(--warning-light);
	}

	.info {
		background-color: var(--info);
	}
	.info:hover:not(.disabled) {
		background-color: var(--info-light);
	}

	.success {
		background-color: var(--success);
	}
	.success:hover:not(.disabled) {
		background-color: var(--success-light);
	}

</style>
