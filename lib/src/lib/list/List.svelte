<script lang="ts">
	import ListItem from './ListItem.svelte';

	export let checkbox = false;
	export let checked = false;
</script>

<ul>
	{#if checkbox}
		<ListItem size="sm" {checkbox} bind:checked>
			<svelte:fragment>{checked ? 'Unselect all' : 'Select all'}</svelte:fragment>
		</ListItem>
	{/if}
	<slot {checkbox} parentChecked={checked} />
</ul>

<style>
	ul {
		list-style-type: none;
		padding: 0;
		margin: 0;
		display: flex;
		flex-direction: column;
	}
	ul :global(ul) {
		padding-left: 1rem;
	}

	ul > :global(li) {
		min-width: 100px;
	}
	ul > :global(li:not(:last-child)) {
		border-bottom: var(--border-color) 1px solid;
	}
</style>
