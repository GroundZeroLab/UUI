<script lang="ts">
	import type { Size, Status } from '$lib/index.js';

	export let size: Size = undefined;
	export let aspect: string = '';
	export let status: Status = undefined;
	export let disabled: boolean = false;
	$: ar = aspect.split('/');
	$: style = aspect.length > 0 ? `--arw:${ar[0]}; --arh:${ar[1]}` : 'auto';
</script>

<div
	class="box {size ? size : ''}"
	class:disabled
	style="--bd-color:{status ? `var(--${status})` : 'var(--border-color)'}; {style}"
>
	{#if $$slots.title}
		<header>
			<slot name="title" />
		</header>
	{/if}
	{#if $$slots.default}
		<div class="content">
			<slot />
		</div>
	{/if}
	{#if $$slots.footer}
		<footer>
			<slot name="footer" />
		</footer>
	{/if}
</div>

<style>
	.box {
		max-width: 95vw;
		width: 100%;
		border: 1px solid var(--bd-color);
		border-radius: var(--border-radius);
		display: flex;
		flex-direction: column;
		aspect-ratio: var(--arw) / var(--arh);
		font-size: var(--font-size-md);
	}

	.sm {
		width: 300px;
	}
	.md {
		width: 500px;
	}
	.lg {
		width: 700px;
	}

	header {
		border-top-left-radius: 4px;
		border-top-right-radius: 4px;
		padding: 0.5rem;
		font-weight: bold;
		font-size: var(--font-size-lg);
	}

	.content {
		padding: 0.5rem;
		flex: 1;
	}

	header + .content {
		border-top: 1px solid var(--bd-color);
	}

	header:empty + .content {
		border-top: none;
	}

	header:empty{
		padding: 0;

	}

	footer {
		border-bottom-left-radius: 4px;
		border-bottom-right-radius: 4px;
		border-top: 1px solid var(--bd-color);
		padding: 0.5rem;
	}

	header + .content:empty,
	footer:empty {
		display: none;
		border-top: none;
		border-bottom: none;
	}

	.disabled {
		opacity: 0.5;
		pointer-events: none;
		cursor: not-allowed;
	}
</style>
