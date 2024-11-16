<script lang="ts">
	import type { Size, Status } from '$lib/index.js';
	import Button from '$lib/input/Button.svelte';
	import { fade } from 'svelte/transition';
	import Card from './Card.svelte';

	export let size: Size = 'md';
	export let status: Status = undefined;
	export let aspect: string | undefined = undefined;
	export let state: boolean = true;
	export let animate: boolean = true;
	export let closeButton = true;
</script>

{#if state}
	<div class="bg" transition:fade={{ duration: animate ? 150 : 0 }}>
		<div class="modal">
			<Card {aspect} {size} {status}>
				<svelte:fragment slot="header">
					<div class="title">
						<span class="left">
							<slot name="title" />
						</span>
					{#if closeButton}
						<span class="right">
							<Button size="sm" type="danger" onClick={() => state = false}>X</Button>
						</span>
					{/if}
					</div>
				</svelte:fragment>

				<slot/>
				<slot name="footer" slot="footer"/>
			</Card>
		</div>
	</div>
{/if}

<style>
	.bg {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.5);
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
	}
	.modal {
		width: fit-content;
		height: fit-content;
		background-color: var(--bg-color);
		border-radius: var(--border-radius);
	}

	.title {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
</style>
