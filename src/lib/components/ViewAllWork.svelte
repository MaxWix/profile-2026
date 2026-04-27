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

<div class="next-project">
	<div class="next-label">next case study</div>
	<h2>What else has Max built?</h2>
	<button onclick={goToWork} aria-label="View all work" class="next-btn">View all work →</button>
</div>

<style>
	/* ─── NEXT ─── */
	.next-project {
		background: var(--sand);
		padding: 80px 48px;
		text-align: center;
	}
	.next-label {
		font-family: 'Caveat', cursive;
		font-size: 15px;
		color: var(--stone);
		letter-spacing: 2px;
		text-transform: uppercase;
		margin-bottom: 16px;
	}
	.next-project h2 {
		font-size: clamp(28px, 5vw, 48px);
		font-weight: 400;
		letter-spacing: -1px;
		margin-bottom: 28px;
	}
	.next-btn {
		display: inline-block;
		font-family: 'Caveat', cursive;
		font-size: 18px;
		color: var(--bark);
		border: 1.5px solid var(--bark);
		padding: 12px 32px;
		border-radius: 100px;
		text-decoration: none;
		cursor: pointer;
		background: none;
		transition: all 0.25s ease;
	}
	.next-btn:hover {
		background: var(--bark);
		color: var(--warm-white);
	}
</style>
