<table>
	<slot></slot>
</table>

<style>
	table {
		width: 100%;
		border-collapse: collapse;
		margin: 1rem 0;
		border: 1px solid var(--border-color);
		border-radius: var(--border-radius);
		border-spacing: 0;
		border-collapse: separate;
		overflow: hidden;
	}

	table :global(th) {
		background-color: var(--bg-color-active);
		color: var(--pure);
		font-weight: bold;
		padding: 0.5rem;
    border-bottom: 1px solid var(--border-color);
	}

	table :global(td) {
		padding: 0.5rem;
		border-bottom: 1px solid var(--border-color);
	}

	table :global(tr:nth-child(even)) {
		background-color: var(--bg-color-active);

	}

	table :global(tr:last-child td) {
		border-bottom: none;
	}
</style>
