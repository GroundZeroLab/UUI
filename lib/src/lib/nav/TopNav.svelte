<nav>
	<slot />
</nav>

<style>
	nav {
		display: flex;
		gap: 15px;
		align-items: baseline;
		padding: 10px 10px 8px 10px;
		background-color: var(--bg-color-hover);
	}

	nav > :global(h1) {
		margin: 0;
	}
	nav :global(*) {
		white-space: nowrap;
	}
</style>
