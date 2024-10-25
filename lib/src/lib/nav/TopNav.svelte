<nav>
	<slot />
</nav>

<style>
	nav {
		display: flex;
		gap: 15px;
		align-items: baseline;
		padding: 10px 10px 8px 10px;
		margin: 0.3rem 0;
		width: calc(100vw - 20px);
		background-color: black;
	}

	nav > :global(h1) {
		margin: 0;
	}
	nav :global(*) {
		white-space: nowrap;
	}
</style>
