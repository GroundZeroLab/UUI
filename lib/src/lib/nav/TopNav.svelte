<nav>
	<slot />
</nav>

<style>
	nav {
		display: flex;
		gap: 15px;
		align-items: baseline;
		padding: 0.8rem 0.8rem 0.6rem 0.8rem;
		padding: 10px 10px 8px 10px;
		width: calc(100vw - 20px);
		background-color: var(--bg-color-hover);
	}

	nav > :global(h1) {
		margin: 0;
	}
	nav :global(*) {
		white-space: nowrap;
	}
</style>
