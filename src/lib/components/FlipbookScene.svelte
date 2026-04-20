<!-- FlipbookScene.svelte -->
<script>
	import { onMount, onDestroy } from 'svelte';

	export let src; // spritesheet path
	export let frameCount; // total frames
	export let frameW; // px width per frame
	export let frameH; // px height per frame
	export let cols; // frames per row
	export let scrollRange = 600; // px of scroll = full anim

	let canvas, ctx, img, wrapper;
	let currentFrame = 0;
	let raf;

	onMount(() => {
		ctx = canvas.getContext('2d');
		img = new Image();
		img.src = src;
		img.onload = () => drawFrame(0);
		window.addEventListener('scroll', onScroll);
	});

	onDestroy(() => {
		window.removeEventListener('scroll', onScroll);
		cancelAnimationFrame(raf);
	});

	function onScroll() {
		cancelAnimationFrame(raf);
		raf = requestAnimationFrame(update);
	}

	function update() {
		const rect = wrapper.getBoundingClientRect();
		const entered = window.innerHeight - rect.top;
		const progress = clamp(entered / scrollRange, 0, 1);
		const frame = Math.floor(progress * (frameCount - 1));
		if (frame !== currentFrame) {
			currentFrame = frame;
			drawFrame(frame);
		}
	}

	function drawFrame(f) {
		const col = f % cols;
		const row = Math.floor(f / cols);
		ctx.clearRect(0, 0, frameW, frameH);
		ctx.drawImage(img, col * frameW, row * frameH, frameW, frameH, 0, 0, frameW, frameH);
	}

	const clamp = (v, lo, hi) => Math.max(lo, Math.min(hi, v));
</script>

<div bind:this={wrapper} class="flipbook-scene">
	<canvas bind:this={canvas} width={frameW} height={frameH} />
</div>

<!-- Usage in +page.svelte: -->
<!-- <FlipbookScene
  src="/animations/builder.png"
  frameCount={24} frameW={400} frameH={400}
  cols={6} scrollRange={800}
/> -->
