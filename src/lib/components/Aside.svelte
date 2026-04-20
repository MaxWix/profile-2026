<script>
	let open = false;
</script>

<div class="aside" class:open>
	<button class="aside-trigger" on:click={() => (open = !open)}>
		<span class="aside-icon">+</span>
		<span class="aside-label"><slot name="label" /></span>
	</button>

	<div class="aside-body" class:aside-body--open={open}>
		<div class="aside-body-inner">
			<slot />
		</div>
	</div>
</div>

<style>
	.aside {
		border: 1.5px solid var(--light-stone, #ede8df);
		border-radius: 6px;
		margin: 28px 0;
		overflow: hidden;
		transition: border-color 0.2s ease;
	}

	.aside.open {
		border-color: var(--clay);
	}

	.aside-trigger {
		width: 100%;
		display: flex;
		align-items: center;
		gap: 12px;
		padding: 16px 20px;
		background: var(--cream);
		border: none;
		cursor: pointer;
		text-align: left;
		transition: background 0.2s ease;
	}

	.aside-trigger:hover {
		background: var(--sand, #f5efe0);
	}

	.aside-icon {
		font-family: 'Caveat', cursive;
		font-size: 22px;
		color: var(--clay);
		line-height: 1;
		flex-shrink: 0;
		width: 20px;
		text-align: center;
		transition: transform 0.3s ease;
		display: inline-block;
	}

	.aside.open .aside-icon {
		transform: rotate(45deg);
	}

	.aside-label {
		font-family: 'Caveat', cursive;
		font-size: 16px;
		color: var(--bark);
		letter-spacing: 0.3px;
	}

	/* ─── ANIMATED BODY ─── */
	.aside-body {
		display: grid;
		grid-template-rows: 0fr;
		transition: grid-template-rows 0.35s ease;
		background: var(--warm-white, #fdfaf4);
		border-top: 0px solid var(--light-stone, #ede8df);
	}

	.aside-body--open {
		grid-template-rows: 1fr;
		border-top-width: 1px;
	}

	/* inner div must have overflow hidden for grid row trick to work */
	.aside-body-inner {
		overflow: hidden;
		padding: 0 24px 0 52px;
		opacity: 0;
		transform: translateY(6px);
		transition:
			opacity 0.3s ease 0.1s,
			transform 0.3s ease 0.1s,
			padding 0.35s ease;
	}

	.aside-body--open .aside-body-inner {
		opacity: 1;
		transform: translateY(0);
		padding: 20px 24px 24px 52px;
	}

	.aside-body-inner :global(p) {
		font-size: 15px;
		line-height: 1.8;
		color: #4a4440;
		margin-bottom: 4px;
	}

	.aside-body-inner :global(ol) {
		margin: 12px 0 16px 20px;
		display: flex;
		flex-direction: column;
		gap: 10px;
	}

	.aside-body-inner :global(li) {
		font-size: 15px;
		line-height: 1.75;
		color: #4a4440;
	}

	.aside-body-inner :global(.catch) {
		margin-top: 16px;
		padding: 12px 16px;
		background: var(--sand, #f5efe0);
		border-left: 3px solid var(--clay);
		border-radius: 0 4px 4px 0;
		font-size: 14px;
		line-height: 1.7;
		color: var(--bark);
		font-style: italic;
	}
</style>
