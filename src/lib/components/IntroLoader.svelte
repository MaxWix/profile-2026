<!-- src/lib/components/IntroLoader.svelte -->
<script>
	import { onMount } from 'svelte';

	let visible = false;
	let done = false;

	onMount(() => {
		visible = true;

		setTimeout(() => {
			done = true;
			setTimeout(() => (visible = false), 600);
		}, 2000);
	});
</script>

{#if visible}
	<div class="overlay" class:fading={done}>
		<img src="/animations/walker-cycle.gif" alt="" class="walker" />
	</div>
{/if}

<style>
	.overlay {
		position: fixed;
		inset: 0;
		background: var(--warm-white);
		z-index: 1000;
		pointer-events: none;
		transition: opacity 0.6s ease;
	}

	.overlay.fading {
		opacity: 0;
	}

	.walker {
		position: absolute;
		bottom: 35%;
		left: 0;
		width: 180px;
		height: auto;
		animation: walk 2s linear forwards;
		transform: translateX(-80px);
	}

	@keyframes walk {
		from {
			transform: translateX(-80px);
		}
		to {
			transform: translateX(100vw);
		}
	}
</style>
