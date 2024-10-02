<script>
	import '$lib/main.css';
	import Button from '$lib/input/Button.svelte';
	import Switch from '$lib/input/Switch.svelte';
	let checked = true;
	
</script>

<div class="groups">
	<div class="group">
		<Button>Default</Button>
		<Button primary>Primary</Button>
		<Button primary={false}>Secondary</Button>
		<Button disabled>Disable</Button>
		<Button disabled primary>Disable Primary</Button>
	</div>

	<div class="group">
		<Switch size="sm" />
		<Switch size="sm" bind:checked />
		<Switch size="md" />
		<Switch size="md" bind:checked />
		<Switch size="lg" />
		<Switch size="lg" bind:checked />
	</div>
</div>

<style>
	.groups {
		display: flex;
		flex-direction: column;
		gap: 2rem;
	}
	.group {
		display: flex;
		flex-direction: row;
		gap: 1rem;
	}
</style>
