<span class="round">
	<span class="icon">?</span>
	<div class="tip">
		<slot />
	</div>
</span>

<style>
	.round {
		position: relative;
		display: inline-block;
		background-color: var(--border-color);
		border-radius: 50%;
		width: 1.1rem;
		height: 1.1rem;
		margin-left: 0.1rem;
	}

	.icon {
		position: relative;
		width: 100%;
		height: 100%;
		color: var(--pure);
		cursor: pointer;
		display: flex;
		justify-content: center;
	}

	.tip {
		position: absolute;
		display: block;
		top: 1.5rem;
		transform: translateX(-40%);
		background-color: var(--border-color);
		color: var(--text-color);
		padding: 0.5rem;
		border-radius: var(--border-radius);
		box-shadow: 0 0 0.5rem rgba(0, 0, 0, 0.5);
		opacity: 0;
		pointer-events: none;
		transition: 0.2s;
	}

	.tip > :global(*) {
		display: block;
	}
	

	.icon:hover + .tip {
		opacity: 1;
	}
</style>
