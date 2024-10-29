<script lang="ts">
	import type { Size, Status } from '$lib/index.js';
	import UpDown from './UpDown.svelte';

	export let name: string = '';

	export let value: number | null = 0;
	export let min: number = 0;
	export let max: number = 100;
	export let step: number = 1;
	export let disabled: boolean = false;
	export let size: Size = 'md';
	export let status: Status = undefined;

	function check(value: number | null) {
		if (disabled || value === null) return null;
		if (value < min) value = min;
		if (value > max) value = max;
		return value;
	}

	$: value = check(value);

	const onChange = (d: boolean) => {
		if (disabled || value === null) return null;
		if (d) value = value + step;
		else value = value - step;
	};
</script>

<UpDown {disabled} {size} {status} {onChange} maxLength={max.toString().length}>
	<input type="number" bind:value {disabled} {name} />
</UpDown>
