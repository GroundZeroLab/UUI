<script lang="ts">
	import type { Size } from '$lib/index.js';
	import Button from './Button.svelte';

	export let size: Size = 'md';
	export let value;
	export let selection;
</script>

<Button onClick={() => (selection = value)} {size}>
	<slot />
</Button>

<style>
</style>
