<script>
	import { onMount } from 'svelte';
	import '$lib/styles/abstracts.css';
	import IntroLoader from '$lib/components/IntroLoader.svelte';

	let activeCard = null;
	const loamBubbles = [
		// LEFT SIDE
		{ type: 'text', text: 'Ethical Technology', x: -50, y: -55, delay: 0 },
		{ type: 'img', src: '/loam-logo.jpg', x: -18, y: 10, delay: 0.12 },
		{ type: 'text', text: 'Product Management', x: -22, y: 95, delay: 0.24 },
		{ type: 'img', src: '/loam-preview-1.png', x: -45, y: 80, delay: 0.36 },
		{ type: 'img', src: '/loam-preview-2.png', x: -55, y: 0, delay: 0.48 },
		// RIGHT SIDE
		{ type: 'img', src: '/loam-product-screens.jpg', x: 107, y: -45, delay: 0.06 },
		{ type: 'text', text: 'Connection limit: 150', x: 140, y: 30, delay: 0.18 },
		{ type: 'img', src: '/loam-preview-3.png', x: 110, y: 60, delay: 0.3 },
		{ type: 'text', text: 'Algorithm free', x: 135, y: 100, delay: 0.42 },
		{ type: 'img', src: '/loam-preview-4.png', x: 107, y: 140, delay: 0.54 }
	];

	const suitableBubbles = [
		// LEFT SIDE
		{ type: 'img', src: '/leaderboard-before-state.jpg', x: -50, y: -55, delay: 0 },
		{ type: 'text', text: 'Legacy → React', x: -22, y: 10, delay: 0.12 },
		{ type: 'img', src: '/leaderboard-new-top3.png', x: -45, y: 35, delay: 0.24 },
		{ type: 'text', text: '6 weeks · 3 sprints', x: -24, y: 90, delay: 0.36 },
		{ type: 'img', src: '/leaderboard-before-filter-1.jpg', x: -20, y: -70, delay: 0.48 },
		// RIGHT SIDE
		{ type: 'img', src: '/leaderboard-new-filter-drawer.png', x: 107, y: -35, delay: 0.06 },
		{ type: 'img', src: '/leaderboard-final.png', x: 135, y: -50, delay: 0.18 },
		{ type: 'text', text: 'Podium Finish', x: 130, y: 60, delay: 0.3 },
		{ type: 'img', src: '/leaderboard-before-filter-2.jpg', x: 125, y: 110, delay: 0.42 },
		{ type: 'text', text: 'Load time < 1s', x: 108, y: 100, delay: 0.54 }
	];

	const kimsBubbles = [
		// LEFT SIDE
		{ type: 'text', text: 'Skip the line', x: -50, y: -55, delay: 0 },
		{ type: 'img', src: '/kims/kimsGoals.jpg', x: -25, y: 10, delay: 0.12 },
		{ type: 'text', text: '11 weeks', x: -45, y: 100, delay: 0.24 },
		{ type: 'img', src: '/kims/lowFiProto.jpg', x: -50, y: 24, delay: 0.36 },
		{ type: 'text', text: 'Order ahead', x: -22, y: -70, delay: 0.48 },
		// RIGHT SIDE
		{ type: 'img', src: '/kims/hiFiProto.jpg', x: 107, y: -45, delay: 0.06 },
		{ type: 'text', text: 'Live queue status', x: 140, y: 0, delay: 0.18 },
		{ type: 'img', src: '/kims/midFiProto.jpg', x: 125, y: 40, delay: 0.3 },
		{ type: 'text', text: 'Field research', x: 145, y: 80, delay: 0.42 },
		{ type: 'img', src: '/kims/userJourney.png', x: 107, y: 90, delay: 0.54 }
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
					}
				});

				// Find the most visible section and activate its dot
				const visible = [...sections]
					.map((s, i) => ({ i, ratio: s.getBoundingClientRect().top }))
					.filter(({ i }) => sections[i].classList.contains('visible'))
					.sort((a, b) => Math.abs(a.ratio) - Math.abs(b.ratio));

				if (visible.length > 0) {
					dots.forEach((d, i) => d.classList.toggle('active', i === visible[0].i));
				}
			},
			{ threshold: [0, 0.1, 0.25, 0.5] }
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

		setTimeout(() => {
			const circle = document.querySelector('.sketch-circle path');
			if (circle) {
				circle.getAnimations().forEach((a) => a.cancel());
				circle.style.strokeDasharray = '480';
				circle.style.strokeDashoffset = '480';
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

<svelte:head>
	<title>Max Wix</title>
</svelte:head>

<div class="grain"></div>
<div class="progress-bar" id="progress"></div>

<nav class="side-nav" id="sideNav">
	<button class="nav-dot active" data-section="0" aria-label="Hero"></button>
	<button class="nav-dot" data-section="1" aria-label="Work"></button>
	<button class="nav-dot" data-section="2" aria-label="About"></button>
	<button class="nav-dot" data-section="3" aria-label="Experience"></button>
</nav>

<!-- 01 HERO -->
<section class="section hero visible" id="s0">
	<div class="hero-layout">
		<div class="section-inner">
			<span class="hero-tag">portfolio · 2026</span>
			<h1>Hi, I'm Max.</h1>
			<p class="body-text">
				A technologist who thinks deeply about the implications of what we build: on the product, on
				the people using it, and on the planet. I embed the right questions into how we evaluate
				ideas, thinking through a solution's implications from every angle and testing the limits of
				technological solutions. I want to build technology that is genuinely good for people and
				makes our planet a better place.
			</p>
			<!-- <div class="flipbook-zone">
				<span class="flipbook-label">✦ flipbook animation here</span>
			</div> -->
		</div>
	</div>

	<!-- <div class="scroll-hint">
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
	</div> -->
</section>

<!-- WORK -->
<section class="section work-teaser" id="s4">
	<div class="section-inner">
		<div class="section-label">Work</div>
		<h2>What I've built</h2>

		<div class="skill-tags">
			<span class="skill-tag">Product Management</span>
			<span class="skill-tag">UX / UI Design</span>
			<span class="skill-tag">Software Engineering</span>
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
							{#if b.type === 'text'}{b.text}{:else}<img
									src={b.src}
									alt=""
									class="bubble-img"
								/>{/if}
						</div>
					{/each}
				{/if}
				<div class="case-visual placeholder-bg">
					<img src="/loam-logo.jpg" alt="Loam" class="case-thumb" />
				</div>
				<div class="case-meta">
					<span class="case-label">PM · Design · Engineering · UX Research</span>
					<div class="case-title">
						Building social media for human connection over algorithmic reach
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
							{#if b.type === 'text'}{b.text}{:else}<img
									src={b.src}
									alt=""
									class="bubble-img"
								/>{/if}
						</div>
					{/each}
				{/if}
				<div class="case-visual placeholder-bg">
					<img src="/suitable-logo.svg" alt="Suitable" class="case-thumb" />
				</div>
				<div class="case-meta">
					<span class="case-label">PM · Design · Engineering</span>
					<div class="case-title">Rethinking Suitable's Leaderboard from the Ground Up</div>
					<div class="case-desc">
						Migrating legacy Angular code to React, solving deep UX friction, and rethinking what
						gamification should actually mean for students.
					</div>
				</div>
				<span class="case-arrow">→</span>
			</a>

			<a
				class="case-card"
				href="/work/kimsDragon"
				on:mouseenter={() => (activeCard = 'case3')}
				on:mouseleave={() => (activeCard = null)}
			>
				{#if activeCard === 'case3'}
					{#each kimsBubbles as b}
						<div
							class="hover-bubble"
							class:hover-bubble--img={b.type === 'img'}
							style="left:{b.x}%; top:{b.y}%; animation-delay:{b.delay}s"
						>
							{#if b.type === 'text'}{b.text}{:else}<img
									src={b.src}
									alt=""
									class="bubble-img"
								/>{/if}
						</div>
					{/each}
				{/if}
				<div class="case-visual placeholder-bg">
					<img src="/kims/kimsHero.png" alt="Kim's Dragon" class="case-thumb" />
				</div>
				<div class="case-meta">
					<span class="case-label">UX Design · UX Research</span>
					<div class="case-title">
						Designing a mobile ordering app for a beloved campus food truck
					</div>
					<div class="case-desc">
						Kim's Dragon had no digital presence and lines that never quit. We designed an app that
						skips the wait without losing the personality.
					</div>
				</div>
				<span class="case-arrow">→</span>
			</a>
		</div>
	</div>
</section>

<!-- PHILOSOPHY / ABOUT -->
<section class="section philosophy" id="s3">
	<div class="section-inner">
		<div class="section-label">Belief</div>
		<h2>Building is core to <br /> <span class="hand-underline">humanity</span>.</h2>
		<!-- <div class="flipbook-zone">
			<span class="flipbook-label">✦ flipbook animation here</span>
		</div> -->
		<p class="body-text builder-text">
			I believe everyone is a builder in some way, shape, or form. I love learning about people's
			passions and how they build to support their ideas. Even more, I love building to support what <em
				>I</em
			> believe in.
		</p>
		<p class="body-text">
			Being a builder in tech means holding <em>unprecedented </em> power. Technologists have an ethical
			duty and social obligation to build with impact in mind. Impact on the individual user, on society,
			on the environment. Technology changes the world for better or worse. We must choose, day in and
			day out, to build technology that makes the world better.
		</p>
	</div>
</section>

<!-- EXPERIENCE -->
<section class="section experience" id="s4-exp">
	<div class="section-inner">
		<div class="section-label">Experience</div>
		<h2>Where I've Built</h2>
		<p class="body-text">
			I'm a 2026 Drexel graduate with a BS in User Experience and Interaction Design. Five years, a
			3.66 GPA, concentrations in sociology, photography, business law, and culinary arts.
		</p>

		<div class="exp-list">
			<div class="exp-item">
				<div class="exp-header">
					<div class="exp-left">
						<div class="exp-role">Junior Product Manager</div>
						<div class="exp-company">Suitable</div>
					</div>
					<div class="exp-date">Sep 2025 – February 2026</div>
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
					<div class="exp-date">Apr 2024 – Sep 2025</div>
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
					<div class="exp-date">Apr 2023 – Apr 2024</div>
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

		<div class="contact-row" id="contact">
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

<style>
	/* ─── PROGRESS BAR ─── */
	.progress-bar {
		position: fixed;
		top: 0;
		left: 0;
		width: 0%;
		height: 3px;
		background: var(--color-accent-primary);
		z-index: var(--z-progress);
		transition: width 0.1s linear;
		border-radius: 0 var(--radius-sm) var(--radius-sm) 0;
	}

	/* ─── GRAIN ─── */
	.grain {
		position: fixed;
		inset: 0;
		pointer-events: none;
		z-index: var(--z-grain);
		opacity: 0.03;
		background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
		background-size: 180px;
	}

	/* ─── SIDE NAV DOTS ─── */
	.side-nav {
		position: fixed;
		right: var(--space-6);
		top: 50%;
		transform: translateY(-50%);
		display: flex;
		flex-direction: column;
		gap: var(--space-3);
		z-index: var(--z-nav);
	}

	.nav-dot {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: var(--color-text-muted);
		opacity: 0.4;
		cursor: pointer;
		transition: all var(--ease-default);
		border: none;
		padding: 0;
	}

	.nav-dot.active {
		background: var(--color-accent-primary);
		opacity: 1;
		transform: scale(1.4);
	}

	/* ─── SECTIONS ─── */
	.section {
		min-height: 95vh;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: var(--space-20) 60px;
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
		max-width: var(--max-width-content);
		width: 100%;
		position: relative;
	}

	/* ─── SECTION LABEL ─── */
	.section-label {
		font-family: var(--font-hand);
		font-size: var(--text-base);
		color: var(--color-accent-tertiary);
		letter-spacing: var(--tracking-wider);
		text-transform: uppercase;
		margin-bottom: var(--space-4);
		display: flex;
		align-items: center;
		gap: var(--space-3);
		position: relative;
		z-index: var(--z-base);
	}

	.section-label::before {
		content: '';
		display: inline-block;
		width: 28px;
		height: 1.5px;
		background: var(--color-accent-tertiary);
		border-radius: var(--radius-sm);
	}

	/* ─── HEADINGS (page-level overrides for clamp) ─── */
	h2 {
		font-size: clamp(30px, 5vw, 44px);
		font-weight: var(--weight-normal);
		line-height: var(--leading-snug);
		margin-bottom: var(--space-6);
		letter-spacing: var(--tracking-tight);
		position: relative;
		z-index: var(--z-base);
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

	/* ─── BODY TEXT ─── */
	.body-text {
		font-size: var(--text-base);
		line-height: var(--leading-loose);
		color: var(--color-text-secondary);
		position: relative;
		z-index: var(--z-base);
		max-width: var(--max-width-content);
	}

	.builder-text {
		margin-bottom: var(--space-3);
	}

	/* ─── HERO ─── */
	.hero {
		min-height: 80vh !important;
	}

	.hero-layout {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: var(--space-12);
		width: 100%;
		max-width: var(--max-width-full);
	}

	.hero-tag {
		font-family: var(--font-hand);
		font-size: var(--text-h6);
		color: var(--color-accent-tertiary);
		letter-spacing: var(--tracking-wider);
		margin-bottom: var(--space-4);
		display: block;
	}

	/* ─── SCROLL HINT ─── */
	.scroll-hint {
		position: absolute;
		bottom: var(--space-10);
		left: 50%;
		transform: translateX(-50%);
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: var(--space-2);
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
		font-family: var(--font-hand);
		font-size: var(--text-small);
		color: var(--color-text-muted);
		letter-spacing: var(--tracking-wider);
		text-transform: uppercase;
	}

	.scroll-arrow {
		width: 22px;
		stroke: var(--color-text-muted);
	}

	/* ─── FLIPBOOK ZONE ─── */
	.flipbook-zone {
		width: 130px;
		height: 100px;
		border: 1.5px dashed var(--color-accent-primary);
		border-radius: var(--radius-md);
		display: flex;
		align-items: center;
		justify-content: center;
		margin: var(--space-8) 0;
		opacity: 0.55;
	}

	.flipbook-label {
		font-family: var(--font-hand);
		font-size: var(--text-small);
		color: var(--color-accent-primary);
		text-align: center;
		line-height: var(--leading-normal);
		padding: var(--space-2) var(--space-3);
	}

	/* ─── WORK TEASER ─── */
	.work-teaser {
		background: var(--color-surface-alt);
	}

	.work-teaser .section-inner {
		max-width: 750px;
	}

	.work-teaser .section-label {
		color: var(--color-accent-secondary);
	}

	.work-teaser .section-label::before {
		background: var(--color-accent-secondary);
	}

	.skill-tags {
		display: flex;
		gap: var(--space-3);
		flex-wrap: wrap;
		margin-bottom: var(--space-8);
	}

	.skill-tag {
		font-family: var(--font-hand);
		font-size: var(--text-base);
		color: var(--color-accent-secondary);
		border: 1px solid var(--color-accent-secondary);
		border-radius: var(--radius-full);
		padding: var(--space-1) var(--space-4);
		opacity: 0.7;
	}

	/* ─── CASE STUDY GRID ─── */
	.case-grid {
		display: flex;
		flex-direction: column;
		gap: var(--space-4);
	}

	.case-card {
		display: grid;
		grid-template-columns: 80px 1fr 24px;
		align-items: center;
		gap: var(--space-5);
		padding: var(--space-5) var(--space-6);
		border: 1.5px solid var(--color-border);
		border-radius: var(--radius-lg);
		background: var(--color-surface);
		text-decoration: none;
		color: var(--color-text-primary);
		transition:
			transform var(--ease-default),
			border-color var(--ease-default);
		position: relative;
		z-index: var(--z-base);
		overflow: visible;
	}

	.case-card:hover {
		transform: translateX(6px);
		border-color: var(--color-border-accent);
	}

	.case-visual {
		width: 80px;
		height: 64px;
		border-radius: var(--radius-md);
		background: var(--color-surface-alt);
		border: 1.5px dashed var(--color-accent-primary);
		display: flex;
		align-items: center;
		justify-content: center;
		flex-shrink: 0;
	}

	.case-placeholder {
		font-family: var(--font-hand);
		font-size: var(--text-h6);
		color: var(--color-accent-primary);
		opacity: 0.6;
	}

	.case-meta {
		display: flex;
		flex-direction: column;
		gap: var(--space-1);
	}

	.case-label-top {
		font-family: var(--font-hand);
		font-size: var(--text-base);
		color: var(--color-accent-secondary);
		margin-bottom: -12px;
	}

	.case-label {
		font-family: var(--font-hand);
		font-size: var(--text-base);
		color: var(--color-text-muted);
		letter-spacing: var(--tracking-wide);
	}

	.case-title {
		font-family: var(--font-serif);
		font-size: var(--text-h5);
		font-weight: var(--weight-medium);
		color: var(--color-text-primary);
		line-height: var(--leading-snug);
	}

	.case-desc {
		font-family: var(--font-serif);
		font-size: var(--text-base);
		color: var(--color-text-muted);
		line-height: var(--leading-snug);
	}

	.case-arrow {
		font-size: var(--text-h6);
		color: var(--color-accent-primary);
		opacity: 0;
		transition:
			opacity var(--ease-default),
			transform var(--ease-default);
	}

	.case-card:hover .case-arrow {
		opacity: 1;
		transform: translateX(4px);
	}

	.case-thumb {
		width: 100%;
		height: 100%;
		border-radius: var(--radius-sm);
	}

	/* ─── HOVER BUBBLES ─── */
	.hover-bubble {
		position: absolute;
		font-family: var(--font-hand);
		font-size: var(--text-small);
		color: var(--color-accent-secondary);
		background: var(--color-surface-alt);
		border: 1px solid var(--color-accent-primary);
		border-radius: var(--radius-full);
		padding: var(--space-1) var(--space-3);
		white-space: nowrap;
		pointer-events: none;
		z-index: var(--z-raised);
		opacity: 0;
		transform: translateY(6px) scale(0.9);
		animation: bubblePop 0.25s ease forwards;
	}

	.hover-bubble--img {
		padding: 3px;
		border-radius: var(--radius-xl);
		background: var(--color-surface);
		width: 92px;
		height: 92px;
		overflow: hidden;
	}

	.bubble-img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: var(--radius-lg);
		display: block;
	}

	@keyframes bubblePop {
		to {
			opacity: 1;
			transform: translateY(0) scale(1);
		}
	}

	/* ─── PHILOSOPHY / ABOUT ─── */
	.philosophy {
		background: var(--color-dark-bg);
	}

	.philosophy .section-label {
		color: var(--sage);
	}

	.philosophy .section-label::before {
		background: var(--sage);
	}

	.philosophy h2 {
		color: var(--color-dark-text);
	}

	.philosophy .body-text {
		color: var(--color-dark-muted);
	}

	/* ─── EXPERIENCE ─── */
	.experience {
		background: var(--color-bg);
		align-items: flex-start;
		padding-top: var(--space-32);
		padding-bottom: var(--space-32);
	}

	.exp-list {
		display: flex;
		flex-direction: column;
		margin: var(--space-8) 0 var(--space-10);
		border-top: 1px solid var(--color-border);
	}

	.exp-item {
		padding: var(--space-6) 0;
		border-bottom: 1px solid var(--color-border);
	}

	.exp-header {
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		gap: var(--space-4);
		margin-bottom: var(--space-3);
	}

	.exp-role {
		font-size: var(--text-h6);
		font-weight: var(--weight-medium);
		color: var(--color-text-primary);
		line-height: var(--leading-snug);
	}

	.exp-company {
		font-family: var(--font-hand);
		font-size: var(--text-base);
		color: var(--color-accent-primary);
		margin-top: var(--space-1);
	}

	.exp-date {
		font-family: var(--font-hand);
		font-size: var(--text-base);
		color: var(--color-accent-secondary);
		white-space: nowrap;
		padding-top: var(--space-1);
		flex-shrink: 0;
	}

	.exp-body {
		font-size: var(--text-base);
		line-height: var(--leading-relaxed);
		color: var(--color-text-secondary);
	}

	/* ─── CONTACT ROW ─── */
	.contact-row {
		display: flex;
		gap: var(--space-3);
		flex-wrap: wrap;
	}

	.contact-link {
		display: flex;
		flex-direction: column;
		gap: var(--space-1);
		padding: var(--space-4) var(--space-5);
		border: 1.5px solid var(--color-border);
		border-radius: var(--radius-lg);
		text-decoration: none;
		color: var(--color-text-primary);
		font-size: var(--text-base);
		background: var(--color-surface);
		transition:
			border-color var(--ease-default),
			transform var(--ease-default);
		flex: 1;
		min-width: 140px;
	}

	.contact-link:hover {
		border-color: var(--color-border-accent);
		transform: translateY(-2px);
	}

	.contact-label {
		font-family: var(--font-hand);
		font-size: var(--text-small);
		color: var(--color-text-muted);
		letter-spacing: var(--tracking-wider);
		text-transform: uppercase;
	}

	/* ─── RESPONSIVE ─── */
	@media (max-width: 900px) {
		.hover-bubble {
			display: none;
		}
	}

	@media (max-width: 600px) {
		.section {
			padding: var(--space-16) var(--space-8);
		}

		.side-nav {
			right: var(--space-4);
		}

		.case-card {
			grid-template-columns: 1fr 20px;
			gap: var(--space-4);
			padding: var(--space-4);
		}

		.case-visual {
			display: none;
		}

		.exp-header {
			flex-direction: column;
			gap: var(--space-1);
		}

		.contact-row {
			flex-direction: column;
		}

		.contact-link {
			min-width: unset;
		}
	}
</style>
