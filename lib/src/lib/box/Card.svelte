<script lang="ts">
	import type { Size, Status } from '$lib/index.js';

	export let size: Size = 'sm';
	export let aspect: string = '';
	export let status: Status = undefined
	$: ar = aspect.split('/');
	$: style = aspect.length > 0 ? `--arw:${ar[0]}; --arh:${ar[1]}` : 'auto';
</script>

<div class="box {size}" 
style="--bd-color:{status ?  `var(--${status})` : 'var(--border-color)'}; {style}">
	{#if $$slots.header}
		<header>
			<slot name="header" />
		</header>
	{/if}
	<div class="content">
		<slot />
	</div>
	{#if $$slots.footer}
		<footer>
			<slot name="footer" />
		</footer>
	{/if}
</div>

<style>
	.sm {
		width: 300px;
	}
	.md {
		width: 500px;
	}
	.lg {
		width: 700px;
	}

	.box {
		max-width: 95vw;
		border: 1px solid var(--bd-color);
		border-radius: var(--border-radius);
		display: flex;
		flex-direction: column;
		aspect-ratio: var(--arw) / var(--arh);
		font-size: var(--font-size-md);
	}

	header {
		border-bottom: 1px solid var(--bd-color);
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
</style>
