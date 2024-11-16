<script lang="ts">
	import type { Size, Status } from '$lib/index.js';
	import UpDown from './UpDown.svelte';

	export let name: string = '';
	export let status: Status = undefined;

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
		const nValue = numberToChar(internalValue);
		if (nValue !== value) return nValue;
		return value.toUpperCase();
	}

	$: value = check(value);
</script>

<UpDown {disabled} {size} {status} {onChange} maxLength={max.toString().length}>
	<input type="text" bind:value class={size} {disabled} {name} />
</UpDown>
