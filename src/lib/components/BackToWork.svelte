<script>
	import { goto } from '$app/navigation';

	async function goToWork() {
		await goto('/');
		// Wait a tick for the page to render, then scroll
		setTimeout(() => {
			const el = document.getElementById('s4');
			if (el) el.scrollIntoView({ behavior: 'smooth' });
		}, 100);
	}
</script>

<button class="back-to-work" onclick={goToWork} aria-label="Back to work">
	<span class="back-arrow">←</span>
	<span class="back-label">back to work</span>
</button>

<style>
	.back-to-work {
		display: inline-flex;
		align-items: center;
		gap: 8px;
		font-family: 'Caveat', cursive;
		font-size: 17px;
		color: var(--stone);
		background: none;
		border: none;
		cursor: pointer;
		padding: 0;
		text-decoration: none;
		transition: color 0.2s ease;
	}

	.back-to-work:hover {
		color: var(--clay);
	}

	.back-arrow {
		transition: transform 0.2s ease;
		display: inline-block;
	}

	.back-to-work:hover .back-arrow {
		transform: translateX(-3px);
	}
</style>
