<script>
	import { onMount } from 'svelte';
	import IntroLoader from '$lib/components/IntroLoader.svelte';

	let activeCard = null;
	const loamBubbles = [
		// LEFT SIDE
		{ type: 'text', text: "Dunbar's number", x: -26, y: -55, delay: 0 },
		{ type: 'img', src: '/loam-logo.jpg', x: -18, y: 10, delay: 0.12 },
		{ type: 'text', text: 'Algorithm free', x: -22, y: 95, delay: 0.24 },
		{ type: 'img', src: '/loam-desirability-1.png', x: -20, y: 165, delay: 0.36 },
		{ type: 'text', text: 'NFC carabiner', x: -24, y: 255, delay: 0.48 },
		// RIGHT SIDE
		{ type: 'img', src: '/loam-product-screens.jpg', x: 107, y: -45, delay: 0.06 },
		{ type: 'text', text: 'Connection limit: 150', x: 108, y: 50, delay: 0.18 },
		{ type: 'img', src: '/loam-desirability-2.png', x: 106, y: 120, delay: 0.3 },
		{ type: 'gif', src: '/walker-cycle.gif', x: 108, y: 205, delay: 0.42 },
		{ type: 'img', src: '/loam-product-screens.jpg', x: 107, y: 290, delay: 0.54 }
	];

	const suitableBubbles = [
		// LEFT SIDE
		{ type: 'img', src: '/leaderboard-before-state.jpg', x: -20, y: -45, delay: 0 },
		{ type: 'text', text: 'Legacy → React', x: -22, y: 40, delay: 0.12 },
		{ type: 'img', src: '/leaderboard-new-top3.png', x: -20, y: 105, delay: 0.24 },
		{ type: 'text', text: '6 weeks · 3 sprints', x: -24, y: 195, delay: 0.36 },
		{ type: 'img', src: '/leaderboard-before-filter-1.jpg', x: -20, y: 260, delay: 0.48 },
		// RIGHT SIDE
		{ type: 'img', src: '/leaderboard-new-filter-drawer.png', x: 107, y: -35, delay: 0.06 },
		{ type: 'img', src: '/leaderboard-final.png', x: 106, y: 50, delay: 0.18 },
		{ type: 'text', text: 'Podium Finish', x: 108, y: 140, delay: 0.3 },
		{ type: 'img', src: '/leaderboard-before-filter-2.jpg', x: 107, y: 200, delay: 0.42 },
		{ type: 'text', text: 'Load time < 1s', x: 108, y: 290, delay: 0.54 }
	];

	onMount(() => {
		const sections = document.querySelectorAll('.section');
		const dots = document.querySelectorAll('.nav-dot');
		const progress = document.getElementById('progress');

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						entry.target.classList.add('visible');
						const idx = [...sections].indexOf(entry.target);
						dots.forEach((d, i) => d.classList.toggle('active', i === idx));
					}
				});
			},
			{ threshold: 0.4 }
		);

		sections.forEach((s) => observer.observe(s));

		window.addEventListener('scroll', () => {
			const total = document.body.scrollHeight - window.innerHeight;
			const pct = total > 0 ? (window.scrollY / total) * 100 : 0;
			progress.style.width = pct + '%';
		});

		dots.forEach((dot) => {
			dot.addEventListener('click', () => {
				const idx = parseInt(dot.dataset.section);
				sections[idx].scrollIntoView({ behavior: 'smooth' });
			});
		});

		// circle — defer until next tick so DOM is fully painted
		setTimeout(() => {
			const circle = document.querySelector('.sketch-circle path');
			if (circle) {
				// cancel any existing animations on this element
				circle.getAnimations().forEach((a) => a.cancel());
				// force the start state in JS, not CSS
				circle.style.strokeDasharray = '480';
				circle.style.strokeDashoffset = '480';
				// now animate from that guaranteed start state
				circle.animate([{ strokeDashoffset: '480' }, { strokeDashoffset: '0' }], {
					duration: 1600,
					delay: 600,
					easing: 'ease',
					fill: 'forwards'
				});
			}
		}, 100);
	});
</script>

<IntroLoader />

<div class="grain"></div>
<div class="progress-bar" id="progress"></div>

<nav class="side-nav" id="sideNav">
	<button class="nav-dot active" data-section="0" aria-label="Hero"></button>
	<button class="nav-dot" data-section="1" aria-label="Builder"></button>
	<button class="nav-dot" data-section="2" aria-label="Curiosity"></button>
	<button class="nav-dot" data-section="3" aria-label="Philosophy"></button>
	<button class="nav-dot" data-section="4" aria-label="Work"></button>
</nav>

<!-- 01 HERO -->
<section class="section hero visible" id="s0">
	<div class="hero-layout">
		<!-- <div class="hero-col-left">
			<div class="photo-float p1">
				<img src="/photos/me-1.jpg" alt="Max" />
			</div>
			<div class="photo-float p2">
				<img src="/photos/me-2.jpg" alt="Max" />
			</div>
		</div> -->

		<div class="section-inner">
			<span class="hero-tag"> portfolio · 2026</span>
			<h1>
				Hi, I'm Max.
				<div class="name-wrapper">
					<span class="name-text"></span>
					<!-- <svg
						class="sketch-circle"
						viewBox="-5 -10 175 95"
						xmlns="http://www.w3.org/2000/svg"
						aria-hidden="true"
					>
						<path
							d="M 30 55 C 16 48, 5 34, 8 19 C 11 5, 32 -5, 62 -3 C 88 -1, 118 -5, 140 7 C 158 18, 160 40, 150 57 C 140 71, 112 77, 80 76 C 54 75, 26 70, 20 63 C 16 57, 22 57, 30 55 Z"
						/>
					</svg> -->
				</div>
			</h1>
			<p class="body-text">
				A technologist who thinks deeply about the implications of what we build: on the product, on
				the people using it, and on the planet. I embed the right questions into how we evaluate
				ideas, thinking through a solution's implications from every angle and testing the limits of
				technological solutions. I want to build technology that is genuinely good for people and
				makes our planet a better place.
			</p>
			<div class="flipbook-zone">
				<span class="flipbook-label">✦ flipbook animation here</span>
			</div>
		</div>
	</div>

	<div class="scroll-hint">
		<span>scroll</span>
		<svg
			class="scroll-arrow"
			viewBox="0 0 22 30"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
			aria-hidden="true"
		>
			<path
				d="M11 2v24M4 20l7 8 7-8"
				stroke-width="1.5"
				stroke-linecap="round"
				stroke-linejoin="round"
			/>
		</svg>
	</div>
</section>

<!-- 02 BUILDER -->
<section class="section builder" id="s1">
	<div class="section-inner">
		<!-- <span class="chapter-num">01</span> -->
		<div class="section-label">Belief</div>
		<h2>Building is core<br />to <span class="hand-underline">humanity</span>.</h2>
		<div class="flipbook-zone">
			<span class="flipbook-label">✦ flipbook animation here</span>
		</div>
		<p class="body-text">
			I believe everyone is a builder in some way, shape, or form. I love learning about people's
			passions and how they build to support their ideas. Even more, I love building to support what <em
				>I</em
			> believe in.
		</p>
	</div>
</section>

<!-- 03 DISCIPLINES -->
<!-- <section class="section disciplines" id="s2">
	<div class="section-inner">
		<span class="chapter-num">02</span>
		<div class="section-label">curiosity</div>
		<h2>I never could commit<br />to just one minor.</h2>
		<p class="body-text">
			Five years at Drexel. Thousands of hours. An unreasonable number of subjects.
		</p>
		<div class="disc-grid">
			<div class="disc-card sociology">
				<span class="disc-icon">◎</span>
				<div class="disc-title">Sociology &amp; Psychology</div>
				<div class="disc-tag">Social construction · human systems · why we do what we do</div>
			</div>
			<div class="disc-card law">
				<span class="disc-icon">§</span>
				<div class="disc-title">Law</div>
				<div class="disc-tag">Collective power · policy as design · strength in structure</div>
			</div>
			<div class="disc-card photography">
				<span class="disc-icon">⌀</span>
				<div class="disc-title">Medium-Format Film</div>
				<div class="disc-tag">Presence · no predication · light reveals meaning</div>
			</div>
			<div class="disc-card culinary">
				<span class="disc-icon">~</span>
				<div class="disc-title">Culinary Arts</div>
				<div class="disc-tag">Making food for people is one way I express love</div>
			</div>
		</div>
	</div>
</section> -->

<!-- 05 WORK TEASER -->
<section class="section work-teaser" id="s4">
	<div class="section-inner">
		<div class="section-label">Work</div>
		<h2>What I've built</h2>

		<div class="skill-tags">
			<span class="skill-tag">Product Management</span>
			<span class="skill-tag">UX / UI Design</span>
			<span class="skill-tag">Front-End Engineering</span>
		</div>

		<div class="case-grid">
			<a
				class="case-card"
				href="/work/loam"
				on:mouseenter={() => (activeCard = 'loam')}
				on:mouseleave={() => (activeCard = null)}
			>
				{#if activeCard === 'loam'}
					{#each loamBubbles as b}
						<div
							class="hover-bubble"
							class:hover-bubble--img={b.type === 'img' || b.type === 'gif'}
							style="left:{b.x}%; top:{b.y}%; animation-delay:{b.delay}s"
						>
							{#if b.type === 'text'}
								{b.text}
							{:else if b.type === 'gif'}
								<img src={b.src} alt="" class="bubble-img" />
							{:else}
								<img src={b.src} alt="" class="bubble-img" />
							{/if}
						</div>
					{/each}
				{/if}
				<div class="case-visual placeholder-bg">
					<img src="/loam-logo.jpg" alt="Loam" class="case-thumb" />
				</div>
				<div class="case-meta">
					<span class="case-label">PM · Design · Engineering · UX Research</span>
					<div class="case-title">
						Building social media around real human connection rather than algorithmic reach
					</div>
					<div class="case-desc">
						Social media was built to help us connect like never before. But in an age where we
						often feel more isolated and disconnected than ever, something needed to change.
					</div>
				</div>
				<span class="case-arrow">→</span>
			</a>

			<a
				class="case-card"
				href="/work/suitable"
				on:mouseenter={() => (activeCard = 'suitable')}
				on:mouseleave={() => (activeCard = null)}
			>
				{#if activeCard === 'suitable'}
					{#each suitableBubbles as b}
						<div
							class="hover-bubble"
							class:hover-bubble--img={b.type === 'img' || b.type === 'gif'}
							style="left:{b.x}%; top:{b.y}%; animation-delay:{b.delay}s"
						>
							{#if b.type === 'text'}
								{b.text}
							{:else if b.type === 'gif'}
								<img src={b.src} alt="" class="bubble-img" />
							{:else}
								<img src={b.src} alt="" class="bubble-img" />
							{/if}
						</div>
					{/each}
				{/if}
				<div class="case-visual">
					<div class="case-placeholder">✦</div>
				</div>
				<div class="case-meta">
					<span class="case-label">PM · Design · Engineering</span>
					<div class="case-title">Rebuilding the Suitable leaderboard</div>
					<div class="case-desc">
						Migrating legacy Angular to React, solving deep UX friction, and rethinking
						gamification.
					</div>
				</div>
				<span class="case-arrow">→</span>
			</a>

			<a
				class="case-card"
				href="#"
				on:mouseenter={() => (activeCard = 'case3')}
				on:mouseleave={() => (activeCard = null)}
			>
				<div class="case-visual placeholder-bg">
					<div class="case-placeholder">✦</div>
				</div>
				<div class="case-meta">
					<span class="case-label">Coming soon</span>
					<div class="case-title">Case Study 03</div>
					<div class="case-desc">Title and description coming soon.</div>
				</div>
				<span class="case-arrow">→</span>
			</a>
		</div>
	</div>
</section>

<!-- 04 PHILOSOPHY -->
<section class="section philosophy" id="s3">
	<div class="section-inner">
		<h2>Being a builder in tech<br />means holding unprecedented power.</h2>
		<!-- <blockquote class="pull-quote">
			"What you do is not important. It is who you do it for, and why, that matters."
		</blockquote> -->
		<p class="body-text">
			Technologists have an ethical duty and social obligation to build with impact in mind. Impact
			on the individual user, on society, on the environment. Technology changes the world for
			better or worse. We must choose, day in and day out, to build technology the makes the world
			better.
		</p>
	</div>
</section>

<!-- 05 ABOUT -->
<section class="section about" id="s4">
	<div class="section-inner">
		<div class="section-label">about</div>
		<h2>The person<br />behind the work.</h2>

		<p class="body-text">
			I'm a 2026 Drexel graduate with a BS in User Experience and Interaction Design. Five years, a
			3.68 GPA, concentrations in sociology, photography, business law, and culinary arts.
		</p>

		<div class="exp-list">
			<div class="exp-item">
				<div class="exp-header">
					<div class="exp-left">
						<div class="exp-role">Junior Product Manager</div>
						<div class="exp-company">Suitable</div>
					</div>
					<div class="exp-date">Sep 2025 - February 2026</div>
				</div>
				<div class="exp-body">
					Led the discovery and roadmapping of a new online registration feature, reducing the
					administrative burden on college administrators. Conducted user interviews, competitive
					research, and internal refinement sessions to identify product opportunities and inform
					product strategy. Improved and automated sprint metrics reporting to provide analytics and
					insights tailored specifically to the company's needs.
				</div>
			</div>

			<div class="exp-item">
				<div class="exp-header">
					<div class="exp-left">
						<div class="exp-role">Design Engineer</div>
						<div class="exp-company">Suitable</div>
					</div>
					<div class="exp-date">Apr 2024 - Sep 2025</div>
				</div>
				<div class="exp-body">
					Championed platform-wide accessibility, ensuring web-app's full WCAG AA compliance for the
					first time, adding efficiency to the sales process by reducing time spent on client-side
					accessibility audits. Redesigned and deployed the leaderboard feature and reusable
					components throughout the app. Built internal tools that empowered non-developers to
					perform complex tasks independently.
				</div>
			</div>

			<div class="exp-item">
				<div class="exp-header">
					<div class="exp-left">
						<div class="exp-role">Digital Designer</div>
						<div class="exp-company">Miax Exchange Group</div>
					</div>
					<div class="exp-date">Apr 2023 - Apr 2024</div>
				</div>
				<div class="exp-body">
					Web audits, competitive analysis, and user testing. Led creative on advertising,
					marketing, and educational campaigns. Worked across all departments to meet design needs
					for the company and its subsidiaries.
				</div>
			</div>

			<div class="exp-item">
				<div class="exp-header">
					<div class="exp-left">
						<div class="exp-role">Production Manager & Lead Print Designer</div>
						<div class="exp-company">The Triangle</div>
					</div>
					<div class="exp-date">Dec 2022 - Jan 2025</div>
				</div>
				<div class="exp-body">
					Managed ~80 staff through all aspects of newsprint production. Designed a production
					schedule and strategy still in use today, facilitating a full print publication in just 2
					days.
				</div>
			</div>
		</div>

		<div class="contact-row">
			<a href="mailto:max.wix@drexel.edu" class="contact-link">
				<span class="contact-label">email</span>
				max.wix@drexel.edu
			</a>
			<a href="https://www.linkedin.com/in/max-wix-82002b22b/" target="_blank" class="contact-link">
				<span class="contact-label">linkedin</span>
				max-wix ↗
			</a>
			<a href="/max-wix-resume-2026.pdf" target="_blank" class="contact-link">
				<span class="contact-label">resume</span>
				download ↗
			</a>
		</div>
	</div>
</section>

<footer class="site-footer">
	<span class="footer-text">Built with love and svelte by Max Wix · &#169 2026</span>
</footer>

<style>
	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}

	:root {
		--sand: #f5efe0;
		--clay: #c4956a;
		--bark: #7a5c3e;
		--moss: #6b7c5e;
		--stone: #9e9285;
		--ink: #2e2a24;
		--cream: #faf6ee;
		--warm-white: #fdfaf4;
		--terracotta: #b85c38;
		--sage: #a3b89a;
	}

	html {
		scroll-behavior: smooth;
	}

	body {
		background: var(--warm-white);
		font-family: 'Lora', Georgia, serif;
		color: var(--ink);
		overflow-x: hidden;
	}

	/* ─── PROGRESS BAR ─── */
	.progress-bar {
		position: fixed;
		top: 0;
		left: 0;
		width: 0%;
		height: 3px;
		background: var(--clay);
		z-index: 100;
		transition: width 0.1s linear;
		border-radius: 0 2px 2px 0;
	}

	/* ─── SIDE NAV DOTS ─── */
	.side-nav {
		position: fixed;
		right: 28px;
		top: 50%;
		transform: translateY(-50%);
		display: flex;
		flex-direction: column;
		gap: 12px;
		z-index: 50;
	}

	.nav-dot {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: var(--stone);
		opacity: 0.4;
		cursor: pointer;
		transition: all 0.3s ease;
		border: none;
		padding: 0;
	}
	.nav-dot.active {
		background: var(--clay);
		opacity: 1;
		transform: scale(1.4);
	}

	/* ─── SECTIONS ─── */
	.section {
		min-height: 95vh;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 80px 60px;
		position: relative;
		opacity: 0;
		transform: translateY(40px);
		transition:
			opacity 0.9s ease,
			transform 0.9s ease;
	}
	.section.visible {
		opacity: 1;
		transform: translateY(0);
	}

	.section-inner {
		max-width: 660px;
		width: 100%;
		position: relative;
	}

	/* ─── HAND-DRAWN UNDERLINE ─── */
	.hand-underline {
		position: relative;
		display: inline-block;
	}
	.hand-underline::after {
		content: '';
		position: absolute;
		bottom: -4px;
		left: -4px;
		right: -4px;
		height: 8px;
		background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 8'%3E%3Cpath d='M2 5 Q20 2 40 5 Q60 8 80 4 Q100 1 120 5 Q140 8 160 4 Q180 1 198 5' stroke='%23C4956A' stroke-width='2' fill='none' stroke-linecap='round'/%3E%3C/svg%3E")
			repeat-x center;
		background-size: auto 100%;
		opacity: 0.8;
	}

	/* ─── HERO LAYOUT ─── */
	.hero-layout {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 48px;
		width: 100%;
		max-width: 960px;
	}

	.hero-col-left {
		display: flex;
		flex-direction: column;
		gap: 16px;
		flex-shrink: 0;
		align-items: flex-end;
		padding-top: 40px;
	}

	@media (max-width: 900px) {
		.hero-col-left {
			display: none;
		}
		.hero-layout {
			gap: 0;
		}
	}

	.hero-tag {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		color: var(--moss);
		letter-spacing: 1.5px;
		margin-bottom: 14px;
		display: block;
	}

	/* ─── FLOATING PHOTOS ─── */
	.photo-float {
		overflow: hidden;
		opacity: 0;
		flex-shrink: 0;
	}

	.photo-float img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		display: block;
		filter: saturate(0.8);
		transition:
			filter 0.3s ease,
			transform 0.4s ease;
	}

	.photo-float:hover img {
		filter: saturate(1);
		transform: scale(1.04);
	}

	.p1 {
		width: 160px;
		height: 190px;
		clip-path: path(
			'M 90 0 C 140 0, 160 35, 158 85 C 156 135, 130 192, 78 190 C 26 188, 0 148, 2 90 C 4 32, 40 0, 90 0 Z'
		);
		animation:
			floatIn 0.8s ease forwards 0.1s,
			drift1 7s ease-in-out infinite 1s;
	}

	.p2 {
		width: 140px;
		height: 170px;
		clip-path: path(
			'M 70 0 C 118 0, 142 30, 140 80 C 138 130, 112 170, 62 168 C 12 166, 0 128, 2 75 C 4 22, 22 0, 70 0 Z'
		);
		animation:
			floatIn 0.8s ease forwards 0.3s,
			drift2 9s ease-in-out infinite 1.2s;
	}

	.p4 {
		width: 150px;
		height: 200px;
		clip-path: path(
			'M 75 2 C 122 0, 150 34, 148 88 C 146 142, 116 200, 65 198 C 14 196, 0 152, 2 92 C 4 32, 28 4, 75 2 Z'
		);
		animation:
			floatIn 0.8s ease forwards 0.5s,
			drift3 8s ease-in-out infinite 1.4s;
	}

	@keyframes floatIn {
		from {
			opacity: 0;
			transform: translateY(24px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	@keyframes drift1 {
		0%,
		100% {
			transform: translateY(0px) rotate(-2deg);
		}
		50% {
			transform: translateY(-10px) rotate(-0.5deg);
		}
	}
	@keyframes drift2 {
		0%,
		100% {
			transform: translateY(0px) rotate(1.5deg);
		}
		50% {
			transform: translateY(-14px) rotate(3deg);
		}
	}
	@keyframes drift3 {
		0%,
		100% {
			transform: translateY(0px) rotate(-1deg);
		}
		50% {
			transform: translateY(-10px) rotate(-3deg);
		}
	}

	@media (max-width: 900px) {
		.hero-col-left,
		.hero-col-right {
			display: none;
		}
		.hero-layout {
			gap: 0;
		}
	}

	/* Animated sketch circle */
	.name-wrapper {
		position: relative;
		display: inline-block;
		padding: 0 8px;
	}

	.sketch-circle {
		position: absolute;
		top: -18px;
		left: -20px;
		width: calc(100% + 40px);
		height: calc(100% + 36px);
		pointer-events: none;
		overflow: visible;
	}

	.sketch-circle path {
		stroke: var(--clay);
		stroke-width: 2.5;
		fill: none;
		stroke-linecap: round;
		stroke-linejoin: round;
		stroke-dasharray: 480;
		stroke-dashoffset: 480;
	}

	:global(.sketch-circle path.animate) {
		animation: drawCircle 1.6s ease forwards 0.6s;
	}

	@keyframes drawCircle {
		to {
			stroke-dashoffset: 0;
		}
	}

	/* Flipbook placeholder */
	.flipbook-zone {
		width: 130px;
		height: 100px;
		border: 1.5px dashed var(--clay);
		border-radius: 6px;
		display: flex;
		align-items: center;
		justify-content: center;
		margin: 28px 0;
		opacity: 0.55;
	}
	.flipbook-label {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		color: var(--clay);
		text-align: center;
		line-height: 1.5;
		padding: 10px;
	}

	/* ─── SECTION 2: BUILDER ─── */
	.builder {
		background: var(--cream);
	}

	.chapter-num {
		font-family: 'Caveat', cursive;
		font-size: 90px;
		color: var(--sand);
		position: absolute;
		top: -28px;
		left: -24px;
		line-height: 1;
		pointer-events: none;
		font-weight: 600;
		z-index: 0;
	}

	.section-label {
		font-family: 'Caveat', cursive;
		font-size: 16px;
		color: var(--moss);
		letter-spacing: 1.5px;
		text-transform: uppercase;
		margin-bottom: 14px;
		display: flex;
		align-items: center;
		gap: 10px;
		position: relative;
		z-index: 1;
	}
	.section-label::before {
		content: '';
		display: inline-block;
		width: 28px;
		height: 1.5px;
		background: var(--moss);
		border-radius: 2px;
	}

	h2 {
		font-size: clamp(30px, 5vw, 44px);
		font-weight: 400;
		line-height: 1.2;
		margin-bottom: 24px;
		letter-spacing: -0.5px;
		position: relative;
		z-index: 1;
	}

	.body-text {
		font-size: 17px;
		line-height: 1.85;
		color: #4a4440;
		position: relative;
		z-index: 1;
		max-width: 660px;
	}

	/* ─── SECTION 3: DISCIPLINES ─── */
	.disciplines {
		background: var(--warm-white);
	}

	.disc-grid {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 16px;
		margin-top: 32px;
	}

	.disc-card {
		padding: 22px 24px;
		border: 1.5px solid;
		border-radius: 6px;
		position: relative;
		overflow: hidden;
		cursor: default;
		transition:
			transform 0.3s ease,
			box-shadow 0.3s ease;
		background: transparent;
	}
	.disc-card:hover {
		transform: translateY(-4px);
		box-shadow: 0 12px 32px rgba(0, 0, 0, 0.07);
	}

	.disc-card.sociology {
		border-color: var(--moss);
	}
	.disc-card.law {
		border-color: var(--bark);
	}
	.disc-card.photography {
		border-color: var(--stone);
	}
	.disc-card.culinary {
		border-color: var(--terracotta);
	}

	.disc-icon {
		font-family: 'Caveat', cursive;
		font-size: 30px;
		margin-bottom: 12px;
		display: block;
	}
	.disc-card.sociology .disc-icon {
		color: var(--moss);
	}
	.disc-card.law .disc-icon {
		color: var(--bark);
	}
	.disc-card.photography .disc-icon {
		color: var(--stone);
	}
	.disc-card.culinary .disc-icon {
		color: var(--terracotta);
	}

	.disc-title {
		font-family: 'Lora', serif;
		font-size: 16px;
		font-weight: 500;
		color: var(--ink);
		margin-bottom: 8px;
	}
	.disc-tag {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		color: var(--stone);
		line-height: 1.5;
	}

	/* ─── SECTION 4: PHILOSOPHY ─── */
	.philosophy {
		background: var(--ink);
	}
	.philosophy .section-label {
		color: var(--sage);
	}
	.philosophy .section-label::before {
		background: var(--sage);
	}
	.philosophy h2 {
		color: var(--sand);
	}
	.philosophy .chapter-num {
		color: rgba(255, 255, 255, 0.05);
	}

	.pull-quote {
		font-size: clamp(22px, 3.5vw, 30px);
		font-style: italic;
		line-height: 1.55;
		color: var(--clay);
		border-left: 3px solid var(--clay);
		padding-left: 28px;
		margin: 32px 0;
		font-weight: 400;
	}

	.philosophy .body-text {
		color: #b0a89e;
	}

	/* ─── SECTION 5: WORK TEASER ─── */
	.work-teaser {
		background: var(--sand);
	}
	.work-teaser .section-label {
		color: var(--bark);
	}
	.work-teaser .section-label::before {
		background: var(--bark);
	}

	.work-row {
		display: flex;
		gap: 14px;
		margin-top: 32px;
		flex-wrap: wrap;
	}

	.work-chip {
		padding: 11px 22px;
		border: 1.5px solid var(--bark);
		border-radius: 100px;
		font-family: 'Caveat', cursive;
		font-size: 17px;
		color: var(--bark);
		cursor: pointer;
		transition: all 0.25s ease;
		background: transparent;
		letter-spacing: 0.3px;
	}
	.work-chip:hover {
		background: var(--bark);
		color: var(--warm-white);
		transform: scale(1.04);
	}

	/* ─── SCROLL HINT ─── */
	.scroll-hint {
		position: absolute;
		bottom: 40px;
		left: 50%;
		transform: translateX(-50%);
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 8px;
		opacity: 0.45;
		animation: floatHint 2s ease-in-out infinite;
	}
	@keyframes floatHint {
		0%,
		100% {
			transform: translateX(-50%) translateY(0);
		}
		50% {
			transform: translateX(-50%) translateY(7px);
		}
	}
	.scroll-hint span {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		color: var(--stone);
		letter-spacing: 1.5px;
		text-transform: uppercase;
	}
	.scroll-arrow {
		width: 22px;
		stroke: var(--stone);
	}

	/* ─── GRAIN OVERLAY ─── */
	.grain {
		position: fixed;
		inset: 0;
		pointer-events: none;
		z-index: 200;
		opacity: 0.03;
		background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
		background-size: 180px;
	}

	@media (max-width: 600px) {
		.section {
			padding: 60px 28px;
		}
		.disc-grid {
			grid-template-columns: 1fr;
		}
		.side-nav {
			right: 14px;
		}
	}

	/* ─── SKILL TAGS ─── */
	.skill-tags {
		display: flex;
		gap: 10px;
		flex-wrap: wrap;
		margin-bottom: 36px;
	}

	.skill-tag {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		color: var(--bark);
		border: 1px solid var(--bark);
		border-radius: 100px;
		padding: 4px 14px;
		opacity: 0.7;
	}

	/* ─── CASE STUDY GRID ─── */
	.case-grid {
		display: flex;
		flex-direction: column;
		gap: 16px;
	}

	.case-card {
		display: grid;
		grid-template-columns: 80px 1fr 24px;
		align-items: center;
		gap: 20px;
		padding: 20px 24px;
		border: 1.5px solid var(--light-stone, #ede8df);
		border-radius: 8px;
		background: var(--cream);
		text-decoration: none;
		color: var(--ink);
		transition:
			transform 0.25s ease,
			border-color 0.25s ease;
		position: relative;
		z-index: 1;
	}

	.case-card:hover {
		transform: translateX(6px);
		border-color: var(--clay);
	}

	.case-visual {
		width: 80px;
		height: 64px;
		border-radius: 6px;
		background: var(--sand);
		border: 1.5px dashed var(--clay);
		display: flex;
		align-items: center;
		justify-content: center;
		flex-shrink: 0;
	}

	.case-placeholder {
		font-family: 'Caveat', cursive;
		font-size: 18px;
		color: var(--clay);
		opacity: 0.6;
	}

	.case-meta {
		display: flex;
		flex-direction: column;
		gap: 4px;
	}

	.case-label {
		font-family: 'Caveat', cursive;
		font-size: 13px;
		color: var(--stone);
		letter-spacing: 0.5px;
	}

	.case-title {
		font-family: 'Lora', serif;
		font-size: 16px;
		font-weight: 500;
		color: var(--ink);
		line-height: 1.3;
	}

	.case-desc {
		font-family: 'Lora', serif;
		font-size: 13px;
		color: var(--stone);
		line-height: 1.6;
		font-style: italic;
	}

	.case-arrow {
		font-size: 18px;
		color: var(--clay);
		opacity: 0;
		transition:
			opacity 0.2s ease,
			transform 0.2s ease;
	}

	.case-card:hover .case-arrow {
		opacity: 1;
		transform: translateX(4px);
	}

	@media (max-width: 600px) {
		.case-card {
			grid-template-columns: 60px 1fr 20px;
			gap: 14px;
			padding: 16px;
		}
		.case-visual {
			width: 60px;
			height: 50px;
		}
	}

	/* ─── ABOUT SECTION ─── */
	.about {
		background: var(--warm-white);
		align-items: flex-start;
		padding-top: 120px;
		padding-bottom: 120px;
	}

	.exp-list {
		display: flex;
		flex-direction: column;
		gap: 0;
		margin: 36px 0 40px;
		border-top: 1px solid var(--light-stone, #ede8df);
	}

	.exp-item {
		padding: 24px 0;
		border-bottom: 1px solid var(--light-stone, #ede8df);
	}

	.exp-header {
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		gap: 16px;
		margin-bottom: 10px;
	}

	.exp-role {
		font-size: 16px;
		font-weight: 500;
		color: var(--ink);
		line-height: 1.3;
	}

	.exp-company {
		font-family: 'Caveat', cursive;
		font-size: 15px;
		color: var(--clay);
		margin-top: 3px;
	}

	.exp-date {
		font-family: 'Caveat', cursive;
		font-size: 13px;
		color: var(--stone);
		white-space: nowrap;
		padding-top: 2px;
		flex-shrink: 0;
	}

	.exp-body {
		font-size: 15px;
		line-height: 1.75;
		color: #4a4440;
	}

	/* ─── CONTACT ROW ─── */
	.contact-row {
		display: flex;
		gap: 12px;
		flex-wrap: wrap;
	}

	.contact-link {
		display: flex;
		flex-direction: column;
		gap: 4px;
		padding: 16px 20px;
		border: 1.5px solid var(--light-stone, #ede8df);
		border-radius: 8px;
		text-decoration: none;
		color: var(--ink);
		font-size: 15px;
		background: var(--cream);
		transition:
			border-color 0.2s ease,
			transform 0.2s ease;
		flex: 1;
		min-width: 140px;
	}

	.contact-link:hover {
		border-color: var(--clay);
		transform: translateY(-2px);
	}

	.contact-label {
		font-family: 'Caveat', cursive;
		font-size: 12px;
		color: var(--stone);
		letter-spacing: 1.5px;
		text-transform: uppercase;
	}

	@media (max-width: 600px) {
		.exp-header {
			flex-direction: column;
			gap: 4px;
		}
		.contact-row {
			flex-direction: column;
		}
		.contact-link {
			min-width: unset;
		}
	}

	.case-thumb {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 4px;
	}

	/* ─── HOVER BUBBLES ─── */
	.case-card {
		overflow: visible;
	}

	.hover-bubble {
		position: absolute;
		font-family: 'Caveat', cursive;
		font-size: 13px;
		color: var(--bark);
		background: var(--sand);
		border: 1px solid var(--clay);
		border-radius: 100px;
		padding: 4px 12px;
		white-space: nowrap;
		pointer-events: none;
		z-index: 10;
		opacity: 0;
		transform: translateY(6px) scale(0.9);
		animation: bubblePop 0.25s ease forwards;
	}

	.hover-bubble--img {
		padding: 3px;
		border-radius: 10px;
		background: var(--cream);
		width: 92px;
		height: 92px;
		overflow: hidden;
	}

	.bubble-img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 8px;
		display: block;
	}

	@keyframes bubblePop {
		to {
			opacity: 1;
			transform: translateY(0) scale(1);
		}
	}

	/* disable entirely on small screens */
	@media (max-width: 900px) {
		.hover-bubble {
			display: none;
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
