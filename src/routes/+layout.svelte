<script>
	import '../app.css';

	let { children } = $props();
	let menuOpen = $state(false);

	function scrollTo(id) {
		const el = document.getElementById(id);
		if (el) el.scrollIntoView({ behavior: 'smooth' });
		menuOpen = false;
	}

	function toggleMenu() {
		menuOpen = !menuOpen;
	}
</script>

<svelte:head>
	<link
		href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,500;1,400&family=Caveat:wght@400;600&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<header class="site-header">
	<div class="header-left">
		<span class="header-name">Max Wix</span>
	</div>

	<span class="header-roles">
		<span>Product Manager</span>
		<span class="role-sep">·</span>
		<span>UX Designer</span>
		<span class="role-sep">·</span>
		<span>Software Engineer</span>
	</span>

	<!-- Desktop nav -->
	<nav class="header-nav desktop-nav">
		<button onclick={() => scrollTo('s4')} class="nav-link">Work</button>
		<button onclick={() => scrollTo('s3')} class="nav-link">About</button>
		<button onclick={() => scrollTo('s4-exp')} class="nav-link">Experience</button>
		<button onclick={() => scrollTo('contact')} class="nav-link">Contact</button>
	</nav>

	<!-- Hamburger button (mobile/tablet only) -->
	<button
		class="hamburger"
		onclick={toggleMenu}
		aria-label={menuOpen ? 'Close menu' : 'Open menu'}
		aria-expanded={menuOpen}
	>
		<span class="bar" class:open={menuOpen}></span>
		<span class="bar" class:open={menuOpen}></span>
		<span class="bar" class:open={menuOpen}></span>
	</button>
</header>

<!-- Mobile drawer -->
{#if menuOpen}
	<!-- svelte-ignore a11y_click_events_have_key_events a11y_no_static_element_interactions -->
	<div class="mobile-overlay" onclick={() => (menuOpen = false)}></div>
{/if}

<nav class="mobile-nav" class:mobile-nav--open={menuOpen}>
	<button onclick={() => scrollTo('s4')} class="mobile-nav-link">Work</button>
	<button onclick={() => scrollTo('s3')} class="mobile-nav-link">About</button>
	<button onclick={() => scrollTo('s4-exp')} class="mobile-nav-link">Experience</button>
	<button onclick={() => scrollTo('contact')} class="mobile-nav-link">Contact</button>
</nav>

<div class="app">
	<main>
		{@render children()}
	</main>
	<footer class="site-footer">
		<span class="footer-text">Built with love and svelte by Max Wix · &#169 2026</span>
	</footer>
</div>

<style>
	:global(*) {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}

	:global(:root) {
		--sand: #f5efe0;
		--clay: #c4956a;
		--bark: #7a5c3e;
		--moss: #6b7c5e;
		--stone: #9e9285;
		--ink: #2e2a24;
		--cream: #faf6ee;
		--warm-white: #fdfaf4;
	}

	/* ─── HEADER ─── */
	.site-header {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 90;
		display: grid;
		grid-template-columns: 1fr auto 1fr;
		align-items: center;
		padding: 18px 48px;
		background: rgba(253, 250, 244, 0.88);
		backdrop-filter: blur(12px);
		-webkit-backdrop-filter: blur(12px);
		border-bottom: 1px solid rgba(196, 149, 106, 0.15);
	}

	.header-left {
		display: flex;
		align-items: center;
	}

	.header-name {
		font-family: 'Lora', Georgia, serif;
		font-size: 16px;
		font-weight: 500;
		color: var(--ink);
		letter-spacing: -0.2px;
	}

	.header-roles {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		color: var(--bark);
		display: flex;
		align-items: center;
		gap: 6px;
		letter-spacing: 0.2px;
		white-space: nowrap;
	}

	.role-sep {
		color: var(--clay);
		opacity: 0.6;
	}

	/* ─── DESKTOP NAV ─── */
	.header-nav {
		display: flex;
		align-items: center;
		justify-content: flex-end;
		gap: 6px;
	}

	.nav-link {
		font-family: 'Lora', Georgia, serif;
		font-size: 15px;
		color: var(--bark);
		background: none;
		border: none;
		cursor: pointer;
		padding: 6px 14px;
		border-radius: 100px;
		letter-spacing: 0.4px;
		transition:
			color 0.2s ease,
			background 0.2s ease;
	}

	.nav-link:hover {
		color: var(--bark);
		background: rgba(196, 149, 106, 0.1);
	}

	/* ─── HAMBURGER ─── */
	.hamburger {
		display: none;
		flex-direction: column;
		justify-content: center;
		align-items: flex-end;
		gap: 5px;
		width: 36px;
		height: 36px;
		background: none;
		border: none;
		cursor: pointer;
		padding: 4px;
		margin-left: auto;
		z-index: 95;
	}

	.bar {
		display: block;
		height: 1.5px;
		background: var(--bark);
		border-radius: 2px;
		transition: all 0.3s ease;
		transform-origin: center;
	}

	/* three bars at different widths for a refined look */
	.bar:nth-child(1) {
		width: 22px;
	}
	.bar:nth-child(2) {
		width: 16px;
	}
	.bar:nth-child(3) {
		width: 22px;
	}

	/* animate to X when open */
	.bar.open:nth-child(1) {
		width: 20px;
		transform: translateY(6.5px) rotate(45deg);
	}
	.bar.open:nth-child(2) {
		opacity: 0;
		transform: scaleX(0);
	}
	.bar.open:nth-child(3) {
		width: 20px;
		transform: translateY(-6.5px) rotate(-45deg);
	}

	/* ─── MOBILE NAV DRAWER ─── */
	.mobile-nav {
		display: none;
		position: fixed;
		top: 57px; /* just below header */
		right: 0;
		z-index: 88;
		flex-direction: column;
		background: rgba(253, 250, 244, 0.97);
		backdrop-filter: blur(16px);
		-webkit-backdrop-filter: blur(16px);
		border-left: 1px solid rgba(196, 149, 106, 0.15);
		border-bottom: 1px solid rgba(196, 149, 106, 0.15);
		border-radius: 0 0 0 12px;
		padding: 12px 8px;
		min-width: 180px;
		transform: translateX(110%);
		transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.mobile-nav--open {
		transform: translateX(0);
	}

	.mobile-nav-link {
		font-family: 'Lora', Georgia, serif;
		font-size: 17px;
		color: var(--bark);
		background: none;
		border: none;
		cursor: pointer;
		padding: 13px 20px;
		text-align: left;
		border-radius: 8px;
		letter-spacing: 0.2px;
		transition:
			color 0.2s ease,
			background 0.2s ease;
	}

	.mobile-nav-link:hover {
		background: rgba(196, 149, 106, 0.1);
	}

	/* ─── OVERLAY ─── */
	.mobile-overlay {
		display: none;
		position: fixed;
		inset: 0;
		z-index: 85;
		background: transparent;
	}

	/* ─── APP OFFSET ─── */
	.app {
		padding-top: 68px;
	}

	/* ─── RESPONSIVE: tablet + mobile (≤900px) ─── */
	@media (max-width: 900px) {
		.site-header {
			grid-template-columns: 1fr auto auto;
			padding: 16px 24px;
			gap: 0;
		}

		.header-roles {
			display: none; /* hide roles on mobile to keep header clean */
		}

		.desktop-nav {
			display: none;
		}

		.hamburger {
			display: flex;
		}

		.mobile-nav {
			display: flex;
		}

		.mobile-overlay {
			display: block;
		}
	}

	/* ─── FOOTER ─── */
	.site-footer {
		padding: 32px 48px;
		text-align: center;
		background: var(--warm-white);
		border-top: 1px solid var(--light-stone, #ede8df);
	}

	.footer-text {
		font-family: 'Caveat', cursive;
		font-size: 15px;
		color: var(--stone);
		letter-spacing: 0.5px;
	}
</style>
