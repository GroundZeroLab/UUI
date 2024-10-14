<script lang="ts">
	export let id = '';
	export let name = '';
	export let value = '';
	export let placeholder = '';
	export let disabled = false;
	export let size = 'md';
  export let cols= 20;
  export let rows= 3;

	function onInput(e: Event & { currentTarget: EventTarget & HTMLTextAreaElement }) {
		if (!e || !e.target) return;
		//@ts-ignore
		value = e.target.value;
	}
</script>

<textarea

	{name}
	{id}
	{placeholder}
	{disabled}
  {rows}
  {cols} 
  {value}
	class={size}
	on:input={onInput}
/>

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
	textarea {
		border: 1px solid var(--border-color);
		border-radius: var(--border-radius);
		padding: 8px;
		background-color: var(--bg-color);
		color: var(--text-color);
		font-size: var(--font-size-md);
		height: fit-content;
    min-height: 0.8rem;
	}
	textarea:disabled {
		cursor: not-allowed;
		background-color: transparent;
		color: var(--text-color);
		opacity: 0.5;
	}

	textarea:active,
	textarea:focus {
		border-color: var(--primary-color);
		outline: none;
	}
</style>
