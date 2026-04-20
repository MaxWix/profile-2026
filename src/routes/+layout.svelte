<script>
	import '../app.css';

	let { children } = $props();
</script>

<svelte:head>
	<link
		href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,500;1,400&family=Caveat:wght@400;600&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div class="app">
	<main>
		{@render children()}
	</main>

	<footer></footer>
</div>

<style>
</style>
