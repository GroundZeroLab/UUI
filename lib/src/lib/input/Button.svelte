<script lang="ts">
	import type { Size } from '$lib/index.js';

	export let action: 'button' | 'submit' | 'reset' = 'button';
	export let type: 'danger' | 'warning' | 'info' | 'success' | 'icon' | '' = '';
	export let primary: boolean = false;
	export let disabled: boolean = false;

	export let size: Size = 'md';
	export let onClick: () => void = () => {};
</script>

<button
	type={action}
	class:typed={type}
	class:primary
	class:disabled
	class="{size} {type}"
	on:click={disabled ? undefined : onClick}
>
	<slot />
</button>

<style>
	.sm {
		font-size: var(--font-size-sm);
	}

	.md {
		height: fit-content;
		font-size: var(--font-size-md);
	}

	.lg {
		height: 2rem;
		font-size: var(--font-size-lg);
	}

	:global(:root) {
		--button-bg-color: var(--primary-color);
		--button-bg-color-hover: rgb(22, 94, 255);
		--button-text-color: #ffffff;
	}

	button {
		background-color: var(--primary-bg-color);
		border: 1px solid var(--border-color);
		font-weight: bold;
		padding: 0.3rem 0.6rem;
		border-radius: var(--border-radius);
		cursor: pointer;
		transition: 0.2s;
		color: var(--pure);
	}

	button:hover:not(.disabled) {
		border-color: var(--primary-color);
	}

	button.primary {
		background-color: var(--button-bg-color);
		color: var(--button-text-color);
		border-color: var(--button-bg-color);
	}

	button.primary:hover:not(.disabled) {
		border-color: var(--primary-color);
		background-color: var(--bg-color);
		color: var(--pure);
	}
	button.disabled {
		cursor: not-allowed;
		background-color: transparent;
		color: var(--text-color);
		opacity: 0.6;
	}

	.typed {
		color: var(--bg-color);
		border-color: transparent;
	}

	.typed:hover:not(.disabled) {
		color: var(--bg-color);
		border-color: transparent;
	}

	.danger {
		background-color: var(--danger);
	}
	.danger:hover:not(.disabled) {
		background-color: var(--danger-dark);
	}

	.warning {
		background-color: var(--warning);
	}
	.warning:hover:not(.disabled) {
		background-color: var(--warning-dark);
	}

	.info {
		background-color: var(--info);
	}
	.info:hover:not(.disabled) {
		background-color: var(--info-dark);
	}

	.success {
		background-color: var(--success);
	}
	.success:hover:not(.disabled) {
		background-color: var(--success-dark);
	}

	.icon {
		color: var(--pure);
		background-color: transparent;
		padding: 0;
		border: none;
	}
	.icon:hover:not(.disabled) {
		color: var(--primary-color);
		fill: var(--primary-color);
	}

	.icon.sm {
		font-size: 0.6rem;
	}

	.icon.md {
		font-size: 0.7rem;
	}

	.icon.lg {
		font-size: 0.75rem;
	}
</style>
