<script lang="ts">
	import '$lib/main.css';
	import Button from '$lib/input/Button.svelte';
	import Switch from '$lib/input/Switch.svelte';
	import Text from '$lib/input/Text.svelte';
	import Card from '$lib/box/Card.svelte';
	import ListItem from '$lib/list/ListItem.svelte';
	import List from '$lib/list/List.svelte';
	import Accordion from '$lib/box/Accordion.svelte';
	import Loading from '$lib/gauche/Loading.svelte';
	import ProgressBar from '$lib/gauche/ProgressBar.svelte';
	import Tooltip from '$lib/extra/Tooltip.svelte';
	import Numer from '$lib/input/Numeric.svelte';
	import Char from '$lib/input/Char.svelte';
	import RadioElement from '$lib/input/RadioElement.svelte';

	let checked = true;
	let value = '';
	let numberValue = 0;
	let charValue = 'A';

	let clicked = false;
	let selectMode = false;
	let progress = 0;
	let progressDirection = 5;

	let inter: undefined | number;

	$: {
		clearInterval(inter);
		inter = setInterval(() => {
			progress = progress + progressDirection;
			if (progress === 105) progressDirection = -5;
			if (progress === -5) progressDirection = 5;
		}, 1000);
	}

	function onClick() {
		clicked = true;

		setTimeout(() => {
			clicked = false;
		}, 300);
	}
</script>

<div class="groups">
	<div class="groups">
		<div class="group">
			<h2>Button - {clicked}</h2>
			<div class="break" />
			<Button primary={false} size="lg" {onClick}>Secondary</Button>
			<Button primary size="md" {onClick}>Primary</Button>
			<Button disabled size="sm" {onClick}>Disabled</Button>
			<Button disabled size="sm" type="danger" {onClick}>Disabled Danger</Button>
			<div class="break" />
			<Button size="md" type="danger" {onClick}>Danger</Button>
			<Button size="md" type="info" {onClick}>Info</Button>
			<Button size="md" type="success" {onClick}>Sucess</Button>
			<Button size="md" type="warning" {onClick}>Warning</Button>
		</div>
		<div class="group">
			<h2>Switch</h2>
			<div class="break" />
			<Switch size="lg" bind:checked>{checked ? 'On' : 'Off'}</Switch>
			<Switch size="md" bind:checked>{checked ? 'On' : 'Off'}</Switch>
			<Switch size="sm" bind:checked>{checked ? 'On' : 'Off'}</Switch>
		</div>
		<div class="group">
			<h2>Numeric</h2>
			<div class="break" />
			<Numer size="lg" bind:value={numberValue} />
			<Numer bind:value={numberValue} />
			<Numer size="sm" disabled bind:value={numberValue} />
		</div>
		<div class="group">
			<h2>Character - {charValue}</h2>
			<div class="break" />
			<Char size="lg" bind:value={charValue} />
			<Char />
			<Char size="sm" max="Z" value={charValue} />
		</div>
		<div class="group">
			<h2>RadioButton</h2>
			<div class="break" />
			<RadioElement size="lg" group="group1" value="1">Radio 1</RadioElement>
			<RadioElement size="md" group="group1" value="2">Radio 2</RadioElement>
			<RadioElement size="sm" group="group1" value="3" disabled>Radio 3</RadioElement>
		</div>
		<div class="group">
			<h2>Input Text - {value}</h2>
			<div class="break" />
			<Text placeholder="Placeholder" value="Value" disabled size="lg" />
			<Text placeholder="Placeholder" value="Value" hide size="md" />
			<Text placeholder="Placeholder" size="sm" bind:value />
		</div>
	</div>

	<div class="group">
		<h2>Accordion</h2>
		<div class="break" />
		<Accordion>
			<svelte:fragment slot="title">Title</svelte:fragment>
			<svelte:fragment slot="content">
				<span
					>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
					fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
					consectetur deleniti nesciunt architecto minus omnis.
				</span>
			</svelte:fragment>
		</Accordion>
	</div>

	<div class="group">
		<h2>
			List/CheckBox - <Button onClick={() => (selectMode = !selectMode)}
				>{selectMode ? 'List' : 'Selction'}</Button
			>
		</h2>
		<div class="break" />
		<List bind:checkbox={selectMode} let:checkbox let:parentChecked>
			<ListItem size="sm" {checkbox} {parentChecked}>
				<svelte:fragment slot="title">First</svelte:fragment>
				<svelte:fragment slot="at">18:40</svelte:fragment>
				<svelte:fragment slot="subtitle">Subtitle</svelte:fragment>
				<svelte:fragment slot="content"
					>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Libero tenetur tempore dolores
					facilis, ipsum porro, consequatur.</svelte:fragment
				>
			</ListItem>
			<ListItem size="sm" {checkbox} {parentChecked}>
				<svelte:fragment slot="title">Second</svelte:fragment>
			</ListItem>
		</List>
	</div>

	<div class="group">
		<h2>Card</h2>
		<div class="break" />
		<Card size="sm" aspect="">
			<svelte:fragment slot="header">Header</svelte:fragment>
			<svelte:fragment>
				<span
					>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
					fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
					consectetur deleniti nesciunt architecto minus omnis.</span
				>
			</svelte:fragment>
			<svelte:fragment slot="footer">Footer</svelte:fragment>
		</Card>
		<Card size="sm">
			<svelte:fragment slot="header">Header</svelte:fragment>
			<svelte:fragment>
				<span
					>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
					fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
					consectetur deleniti nesciunt architecto minus omnis.</span
				>
			</svelte:fragment>
			<svelte:fragment slot="footer">Footer</svelte:fragment>
		</Card>
		<Card size="lg">
			<span
				>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
				fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
				consectetur deleniti nesciunt architecto minus omnis.
			</span>
		</Card>
	</div>

	<div class="group">
		<h2>Gauge</h2>
		<div class="break" />
		<Loading show={true} showText={false} size="lg" />
		<Loading show={true} showText={true} size="md" />
		<Loading show={true} showText={true} size="sm">Custom</Loading>
		<div class="break" />
		<h2>Progress Bar</h2>
		<div class="break" />
		<ProgressBar value={50} />
		<ProgressBar value={75} />
		<ProgressBar value={progress} />
	</div>

	<div class="group">
		<h2>Tooltip</h2>
		<div class="break" />
		<span>
			Lorem ipsum dolor,<Tooltip>Lorem ipsum dolor,Lorem ipsum dolor</Tooltip>
			sit amet consectetur adipisicing elit. Doloribus minus est a facilis alias laborum
		</span>
	</div>
</div>

<style>
	.groups {
		display: flex;
		flex-direction: column;
		width: 100%;
	}
	.group {
		margin: 0 20px;
		display: flex;
		flex-direction: row;
		gap: 0.25rem 0.5rem;
		flex-wrap: wrap;
		padding-bottom: 1.5em;
		margin-bottom: 1rem;
		align-items: center;
	}
	.group {
		border-bottom: 1px solid var(--border-color);
	}
	.break {
		flex-basis: 100%;
		width: 0;
	}
	h2 {
		padding-bottom: 0.5rem;
		font-size: 1.4rem;
		color: var(--pure);
	}
</style>
