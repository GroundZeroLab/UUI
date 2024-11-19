<script>
	import '$lib/main.css';
	import Button from '$lib/input/Button.svelte';
	import Switch from '$lib/input/Switch.svelte';
	import Text from '$lib/input/Text.svelte';
	import Card from '$lib/box/Card.svelte';
	import ListItem from '$lib/list/ListItem.svelte';
	import List from '$lib/list/List.svelte';
	import Accordion from '$lib/box/Accordion.svelte';
	import Loading from '$lib/gauge/Loading.svelte';
	import ProgressBar from '$lib/gauge/ProgressBar.svelte';
	import Tooltip from '$lib/extra/ToolTip.svelte';
	import Numeric from '$lib/input/Numeric.svelte';
	import Char from '$lib/input/Char.svelte';
	import RadioElement from '$lib/input/RadioElement.svelte';
	import LongText from '$lib/input/LongText.svelte';
	import Modal from '$lib/box/Modal.svelte';
	import TopNav from '$lib/nav/TopNav.svelte';
	import DropDown from '$lib/nav/DropDown.svelte';
	import DropDownLink from '$lib/nav/DropDownLink.svelte';

	let showModal = false;
	let toggle = false;
	let progress = 50;
</script>

<Modal bind:state={showModal} closeButton={false}>
	<h2 slot="title">Modal Title</h2>
	<span>This is a modal content.</span>
	<Button slot="footer" onClick={() => (showModal = false)} type="danger">Close</Button>
</Modal>

<div class="flex-v main">
	<h1>Welcome to this demo of @gzlab/uui</h1>
	<div class="cards">
		{#each new Array(3) as _, i}
			<Card size="sm">
				<svelte:fragment slot="header">Here is a Card {i}</svelte:fragment>
				Lorem ipsum dolor sit amet consectetur adipisicing elit. Earum quasi illo temporibus ratione
				facere beatae quam nobis culpa similique repellat doloribus odio, asperiores tempora? Quo deleniti
				facilis enim rem magnam?
				<span slot="footer">Lorem, ipsum dolor sit amet </span>
			</Card>
		{/each}
		{#each new Array(3) as _, i}
			<Accordion>
				<span slot="title">Accordion Header</span>
				<span slot="content">This is the accordion content.</span>
			</Accordion>
		{/each}
	</div>

	<Card>
		<Button onClick={() => (showModal = true)} primary>Open Modal</Button>
	</Card>

	<Card>
		<List>
			<ListItem>
				Item 1
				<span slot="at">at 12:00</span>
				<span slot="subtitle">Lorem ipsum dolor sit amet</span>
			</ListItem>
			<ListItem>Item 2</ListItem>
			<ListItem>Item 3</ListItem>
		</List>
	</Card>

	<Card>
		<div class="flex">
			<Text placeholder="Enter text" size="md" />
			<Numeric />
			<Char />
		</div>
	</Card>

	<RadioElement group="options" value="1" checked>Option 1</RadioElement>
	<RadioElement group="options" value="2">Option 2</RadioElement>

	<Switch bind:checked={toggle} />

	<ProgressBar value={progress} />
	<Loading />

	<Tooltip>This is a tooltip</Tooltip>
</div>

<style>
	.flex {
		display: flex;
		gap: 0.4rem;
		flex-wrap: wrap;
	}

	.flex-v {
		display: flex;
		gap: 0.4rem;
		flex-direction: column;
	}

	.main {
		padding: 1rem;
		margin: auto;
		max-width: 1200px;
		text-align: center;
	}

	.cards {
		display: flex;
		flex-wrap: wrap;
		gap: 0.3rem;
		justify-content: center;
		align-items: start;
	}
</style>
