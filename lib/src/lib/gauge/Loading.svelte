<script lang="ts">
	import type { Size } from '$lib/index.js';

	export let show = false;
	export let showText = false;
	export let size: Size = 'md';
</script>

{#if show}
	<div class="loading {size}">
		<div class="loadingSpinner"></div>
		<div class="loadingText">
			{#if showText && !$$slots.default}
				Loading...
			{:else}
				<slot />
			{/if}
		</div>
	</div>
{/if}

<style>
	.sm {
		font-size: var(--font-size-sm);
	}
	.sm .loadingSpinner {
		border-width: 0.1rem;
		width: 0.8rem;
		height: 0.8rem;
	}

	.md {
		font-size: var(--font-size-md);
	}
	.md .loadingSpinner {
		width: 1rem;
		height: 1rem;
	}

	.lg {
		font-size: var(--font-size-lg);
	}
	.lg .loadingSpinner {
		border-width: 0.2rem;
		width: 1.2rem;
		height: 1.2rem;
	}

	.loading {
		background-color: transparent;
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 2;
		gap: 0.5rem;
	}

	.loadingSpinner {
		border: 0.15rem solid var(--border-color);
		border-top: 0.15rem solid var(--pure);
		border-radius: 50%;
		width: 1.1rem;
		height: 1.1rem;
		animation: spin 1s linear infinite;
	}

	.loadingText {
		color: var(--text-color);
		margin-bottom: 2%;
	}

	@keyframes spin {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}
</style>
