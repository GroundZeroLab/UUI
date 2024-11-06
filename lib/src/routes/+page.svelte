<script lang="ts">
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
	import Numer from '$lib/input/Numeric.svelte';
	import Char from '$lib/input/Char.svelte';
	import RadioElement from '$lib/input/RadioElement.svelte';
	import LongText from '$lib/input/LongText.svelte';
	import Modal from '$lib/box/Modal.svelte';
	import TopNav from '$lib/nav/TopNav.svelte';
	import DropDown from '$lib/nav/DropDown.svelte';
	import DropDownLink from '$lib/nav/DropDownLink.svelte';

	let checked = true;
	let value = '';
	let numberValue = 0;
	let charValue = 'A';

	let clicked = false;
	let selectMode = false;
	let progress = 0;
	let progressDirection = 5;

	let inter: undefined | number;

	let modalOpen = false;

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

<TopNav>
	<DropDown>
		<div slot="header">DropDown</div>
		<div slot="body" class="grid">
			<DropDownLink href="#">
				📥 Import
				<div slot="description">Import assessment in TAO</div>
			</DropDownLink>
			<DropDownLink href="#">
				📤 Export
				<div slot="description">Export assessment to PDF</div>
			</DropDownLink>
			<DropDownLink href="#">
				⚒️ Forge
				<div slot="description">Create assessment item</div>
			</DropDownLink>
		</div>
	</DropDown>
	<DropDown>
		<div slot="header">DropDown</div>
		<div slot="body" class="grid">
			<DropDownLink href="#">
				📥 Import
				<div slot="description">Import assessment in TAO</div>
			</DropDownLink>
			<DropDownLink href="#">
				📤 Export
				<div slot="description">Export assessment to PDF</div>
			</DropDownLink>
			<DropDownLink href="#">
				⚒️ Forge
				<div slot="description">Create assessment item</div>
			</DropDownLink>
		</div>
	</DropDown>
</TopNav>

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
			<Numer size="lg" bind:value={numberValue} status="danger" />
			<Numer bind:value={numberValue} status="success" />
			<Numer bind:value={numberValue} />
			<Numer size="sm" disabled bind:value={numberValue} status="warning" />
		</div>
		<div class="group">
			<h2>Character - {charValue}</h2>
			<div class="break" />
			<Char size="lg" bind:value={charValue} status="danger" />
			<Char status="success" />
			<Char />
			<Char size="sm" max="Z" value={charValue} status="warning" />
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
			<Text placeholder="Placeholder" value="Value" disabled size="lg" status="danger" />
			<Text placeholder="Placeholder" bind:value size="md" status="success" />
			<Text placeholder="Placeholder" size="sm" bind:value status="warning" />
			<Text placeholder="Placeholder" size="sm" bind:value />
		</div>
		<div class="group">
			<h2>Long text - {value}</h2>
			<div class="break" />
			<LongText placeholder="Placeholder" size="lg" bind:value status="danger" />
			<LongText placeholder="Placeholder" bind:value status="success" />
			<LongText placeholder="Placeholder" size="sm" bind:value status="warning" />
			<LongText placeholder="Placeholder" size="sm" bind:value />
		</div>
	</div>

	<div class="group">
		<h2>Accordion</h2>
		<div class="break" />
		<Accordion status="danger" size="lg">
			<svelte:fragment slot="title">Title</svelte:fragment>
				<span
					>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
					fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
					consectetur deleniti nesciunt architecto minus omnis.
				</span>
		</Accordion>
		<Accordion status="success" size="md">
			<svelte:fragment slot="title">Title</svelte:fragment>
				<span
					>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
					fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
					consectetur deleniti nesciunt architecto minus omnis.
				</span>
		</Accordion>
		<Accordion status="warning" size="sm">
			<svelte:fragment slot="title">Title</svelte:fragment>
				<span
					>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
					fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
					consectetur deleniti nesciunt architecto minus omnis.
				</span>
		</Accordion>
		<Accordion size="sm">
			<svelte:fragment slot="title">Title</svelte:fragment>
				<span
					>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
					fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
					consectetur deleniti nesciunt architecto minus omnis.
				</span>
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
				First
				<svelte:fragment slot="at">18:40</svelte:fragment>
				<svelte:fragment slot="subtitle">Subtitle</svelte:fragment>
				<svelte:fragment slot="content"
					>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Libero tenetur tempore dolores
					facilis, ipsum porro, consequatur.</svelte:fragment
				>
			</ListItem>
			<ListItem size="sm" {checkbox} {parentChecked}>Second</ListItem>
		</List>
	</div>

	<div class="group">
		<h2>Card</h2>
		<div class="break" />
		<Card size="sm" aspect="" status="danger">
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
		<Card size="sm" status="success">
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
		<Card size="lg" status="warning">
			<span
				>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
				fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
				consectetur deleniti nesciunt architecto minus omnis.
			</span>
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

	<div class="group">
		<h2 class="v-align">
			Modal - <Button size="md" onClick={() => (modalOpen = !modalOpen)}>Open</Button>
		</h2>
		<div class="break" />
		<Modal bind:state={modalOpen}>
			<svelte:fragment slot="title">Title</svelte:fragment>
				<span
					>Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis animi dignissimos
					fugiat provident tempora deleniti eligendi ducimus fugit, minus ullam? Tempora dolor illo
					consectetur deleniti nesciunt architecto minus omnis.
				</span>
		</Modal>
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
		align-items: start;
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

	.v-align {
		display: flex;
		gap: 0.5rem;
	}

	.grid {
		display: grid;
		grid-template-columns: repeat(2, 1fr);
	}
</style>
