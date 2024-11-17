<script lang="ts">
	import type { Status } from "$lib/index.js";

	export let id = '';
	export let name = '';
	export let value = '';
	export let placeholder = '';
	export let disabled = false;
	export let size = 'md';
	export let hide = false;
	export let status: Status = undefined

	function onInput(e: Event & { currentTarget: EventTarget & HTMLInputElement }) {
		if (!e || !e.target) return;
		//@ts-ignore
		value = e.target.value;
	}
</script>

<input
	type={hide ? 'password' : 'text'}
	{name}
	{id}
	{placeholder}
	{disabled}
	{value}
	class={`${size}`}
	style="--bd-color:{status ?  `var(--${status})` : 'var(--border-color)'}"
	on:input={onInput}
/>

<style>
	.sm {
		zoom: 0.8;
	}

	.lg {
		zoom: 1.2;
	}

	input {
		border: 1px solid var(--bd-color);
		border-radius: var(--border-radius);
		padding: 5px;
		color: var(--text-color);
		font-size: var(--font-size-md);
	}
	input:disabled {
		cursor: not-allowed;
		background-color: transparent;
		color: var(--text-color);
		opacity: 0.5;
	}

	input:active,
	input:focus {
		border-color: var(--primary-color);
		outline: none;
	}
</style>
