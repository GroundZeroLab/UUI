<script lang="ts">
	export let type: 'button' | 'submit' | 'reset' = 'button';
	export let primary: boolean = false;
	export let disabled: boolean = false;
</script>

<button {type} class:primary class:disabled>
	<slot/>
</button>

<style>
	:global(:root) {
		--button-bg-color: rgb(31, 111, 235);
		--button-bg-color-hover: rgb(22, 94, 255);
		--button-color: #ffffff;
		--button-text-color: #ffffff;
	}

	button {
		background-color: var(--primary-bg-color);
		border: 1px solid var(--border-color);
		color: var(--text-color);
		font-weight: bold;

		padding: 0.5rem 1rem;
		border-radius: 0.5rem;
		cursor: pointer;
		transition: 0.2s;
	}
	button:hover {
		background-color: var(--button-bg-color);
		color: var(--button-text-color);
	}

	button.primary {
		background-color: var(--button-bg-color);
		color: var(--button-text-color);
	}

  button.primary:hover:not(.disabled) {
    background-color: var(--button-bg-color-hover);
  }
	button.disabled {
		cursor: not-allowed;
		background-color: transparent;
		color: var(--text-color);
    opacity: 0.6;
	}
</style>
