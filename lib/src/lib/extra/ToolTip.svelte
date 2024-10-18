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
		top: 1.5rem;
		right: -200%;
		background-color: var(--border-color);
		color: var(--background-color);
		padding: 0.5rem;
		border-radius: var(--border-radius);
		box-shadow: 0 0 0.5rem rgba(0, 0, 0, 0.5);
		opacity: 0;
		pointer-events: none;
		transition: 0.2s;
    width: 10rem;
	}

	.icon:hover + .tip {
		opacity: 1;
	}
</style>
