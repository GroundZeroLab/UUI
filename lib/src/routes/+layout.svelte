<script>
	import List from '$lib/list/List.svelte';
	import ListItem from '$lib/list/ListItem.svelte';
	import DropDown from '$lib/nav/DropDown.svelte';
	import DropDownLink from '$lib/nav/DropDownLink.svelte';
	import SideNav from '$lib/nav/SideNav.svelte';

	import TopNav from '$lib/nav/TopNav.svelte';
</script>

<TopNav>
	<DropDownLink href="/">Home</DropDownLink>
	<DropDown>
		<div slot="header">DropDown</div>
		<div slot="body" class="grid">
			<DropDownLink href="/">
				🏠 Home
				<div slot="description">All component</div>
			</DropDownLink>
			<DropDownLink href="/demo">
				📤 Demo 1
				<div slot="description">A simple demo</div>
			</DropDownLink>
		</div>
	</DropDown>
	<DropDown>
		<div slot="header">DropDown</div>
		<div slot="body" class="grid">
			<DropDownLink href="/">
				🏠 Home
				<div slot="description">All component</div>
			</DropDownLink>
			<DropDownLink href="/demo">
				📤 Demo 1
				<div slot="description">A simple demo</div>
			</DropDownLink>
		</div>
	</DropDown>
</TopNav>

<main>
	<SideNav>
		<List>
			<ListItem>
				<DropDownLink href="#input">
					<h3>Input</h3>
				</DropDownLink>
				<List>
					<ListItem>
						<DropDownLink href="#input-button">Button</DropDownLink>
					</ListItem>
					<ListItem>
						<DropDownLink href="#input-switch">Switch</DropDownLink>
					</ListItem>
					<ListItem>
						<DropDownLink href="#input-numeric">Numeric</DropDownLink>
					</ListItem>
					<ListItem>
						<DropDownLink href="#input-char">Char</DropDownLink>
					</ListItem>
					<ListItem>
						<DropDownLink href="#input-radio-button">RadioButton</DropDownLink>
					</ListItem>
					<ListItem>
						<DropDownLink href="#input-text-field">Text Field</DropDownLink>
					</ListItem>
					<ListItem>
						<DropDownLink href="#input-text-area">Text Area</DropDownLink>
					</ListItem>
				</List>
			</ListItem>
		</List>
	</SideNav>
	<slot />
</main>

<style>
	main {
		height: 100%;
		width: 100%;
		display: flex;
	}
	.grid {
		display: grid;
		grid-template-columns: repeat(2, 1fr);
	}
</style>
