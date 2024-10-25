<nav>
	<slot />
</nav>

<style>
	nav {
		display: flex;
		gap: 15px;
		align-items: baseline;
		padding: 5px 10px;
		width: calc(100vw - 20px);
	}

	nav > :global(h1) {
		margin: 0;
	}

	nav > :global(a) {
		text-decoration: none;
	}

	nav :global(*) {
		/* white-space: nowrap; */
	}
</style>
