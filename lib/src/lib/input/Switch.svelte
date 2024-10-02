<script lang="ts">
	import type { Size } from '$lib/index.js';

	export let checked = false; // The initial state of the switch
	export let size: Size = 'md';
</script>

<label class={size}>
	<input type="checkbox" bind:checked />
	<span class="switch">
		<span class="circle" />
	</span>
</label>

<style>

  .sm{
    zoom: 0.65;
  }

  .md{
    zoom: 0.8;
  }

  .lg{
    zoom: 0.95;
  }

	label {
		width: fit-content;
		height: 25px;
	}
	.switch {
		display: inline-block;
		width: 45px;
		height: 25px;
		background-color: var(--border-color);
		border-radius: 15px;
		position: relative;
		cursor: pointer;
		transition: background-color 0.3s ease;
	}

	.circle {
		position: absolute;
		top: 3px;
		left: 3px;
		height: calc(100% - 6px);
		aspect-ratio: 1;
		border-radius: 50%;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
		transition: transform 0.3s ease;
		background-color: white;
	}

	input[type='checkbox'] {
		display: none;
	}

	input[type='checkbox']:checked + .switch {
		background-color: #68ca6b; /* green when "on" */
	}

	input[type='checkbox']:checked + .switch .circle {
		transform: translateX(101%); /* move the circle to the right when "on" */
	}
</style>
