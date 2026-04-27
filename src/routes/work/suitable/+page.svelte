<script>
	import { onMount } from 'svelte';
	import Aside from '$lib/components/Aside.svelte';
	import BackToWork from '$lib/components/BackToWork.svelte';
	import ViewAllWork from '$lib/components/ViewAllWork.svelte';

	const solutionImages = [
		{ src: '/leaderboard-new-top3.png', caption: 'Podium Finish — top 3 treatment' },
		{ src: '/leaderboard-new-filter-drawer.png', caption: 'Filter drawer — open state' },
		{ src: '/leaderboard-final.png', caption: 'Points breakdown sidebar' }
	];

	let selectedIndex = 0;
	let selectedSolution = solutionImages[0].src;
	let selectedCaption = solutionImages[0].caption;

	onMount(() => {
		const sections = document.querySelectorAll('.cs-section');
		const progress = document.getElementById('progress');

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) entry.target.classList.add('visible');
				});
			},
			{ threshold: 0.12 }
		);

		sections.forEach((s) => observer.observe(s));

		window.addEventListener('scroll', () => {
			const total = document.body.scrollHeight - window.innerHeight;
			const pct = total > 0 ? (window.scrollY / total) * 100 : 0;
			progress.style.width = pct + '%';
		});
	});
</script>

<svelte:head>
	<title>Suitable Leaderboard Rebuild — Max's Portfolio</title>
	<link
		href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,500;1,400&family=Caveat:wght@400;600&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div class="grain"></div>
<div class="progress-bar" id="progress"></div>

<nav class="top-nav">
	<BackToWork />
	<span class="nav-name">Max</span>
</nav>

<!-- ─── HERO ─── -->
<header class="case-hero">
	<div class="hero-bg-text">Suitable</div>
	<div class="hero-content">
		<div class="case-tag">
			<span class="tag-pill pm">Product Management</span>
			<span class="tag-pill ux">UX / UI Design</span>
			<span class="tag-pill dev">Front-End Engineering</span>
		</div>
		<h1>Leaderboard<br /><em>Rebuild</em></h1>
		<p class="subtitle">
			Migrating legacy Angular code to React, solving deep UX friction, and rethinking what
			gamification should actually mean for students.
		</p>
	</div>
</header>

<!-- ─── META STRIP ─── -->
<div class="meta-strip">
	<div class="meta-inner">
		<div class="meta-item">
			<div class="meta-label">Company</div>
			<div class="meta-value">Suitable</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">Timeline</div>
			<div class="meta-value">6 weeks · 3 sprints</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">My Role</div>
			<div class="meta-value">PM, Design, Engineering</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">Scope</div>
			<div class="meta-value">30-40 story points</div>
		</div>
	</div>
</div>

<div class="case-body">
	<!-- 00 CONTEXT -->
	<section class="cs-section" id="context">
		<div class="section-eyebrow">
			<span class="eyebrow-num">00</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Context</span>
		</div>
		<h2>What is Suitable, and why<br />does the leaderboard matter?</h2>
		<p class="body-text">
			Suitable's flagship "Guided Pathways" product helps colleges centralize co-curricular and
			experiential learning opportunities and connect them to students. College Administrators map
			real-world activities to core competencies that reflect each school's mission. When students
			complete activities, they earn a predetermined number of points toward specific competencies.
		</p>
		<p class="body-text">
			The leaderboard was built to gamify this experience: to motivate students individually and in
			groups, and to give the program visibility on campus screens and social media. It was
			high-profile. And it was broken.
		</p>
		<Aside>
			<span slot="label">How is the leaderboard calculated?</span>

			<p>Originally, the leaderboard was calculated using two factors:</p>
			<ol>
				<li>
					<strong>Total Points:</strong> Total points earned from completing activities during a set time
					period.
				</li>
				<li>
					<strong>Student level (1-5):</strong> A status earned by completing a set of activities. By
					completing 3 or more level 1 activities in a competency, students level up to level 2 in that
					area. Once all competency areas reach level 2, the student's overall level increases to 2.
				</li>
			</ol>
			<div class="catch">
				The catch: levels were prioritized over points. A level-2 student with 500 points ranked
				higher than a level-1 student with 750 points.
			</div>
		</Aside>
		<div class="case-img-wrap">
			<img
				src="/leaderboard-before-state.jpg"
				alt="Screenshot of the original leaderboard design, showing a ranked list of students with their points and levels"
				class="case-img"
			/>
			<span class="case-img-caption">The original leaderboard — before the rebuild.</span>
		</div>
	</section>

	<!-- 01 PROBLEM -->
	<section class="cs-section" id="problem">
		<div class="section-eyebrow">
			<span class="eyebrow-num">01</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">The Problem</span>
		</div>
		<h2>Users were frustrated.<br />The code was <span class="hand-underline">exhausted</span>.</h2>
		<p class="body-text">
			I analyzed our full repository of customer feedback — past surveys, CS logs, support tickets,
			in-app data collection. Three problems surfaced repeatedly.
		</p>
		<div class="insight-grid">
			<div class="insight-card" data-num="insight 01">
				<div class="insight-title">Convoluted ranking logic</div>
				<div class="insight-body">
					The leveling system was prioritized over points. A level-2 student with 500 pts outranked
					a level-1 student with 750. Most clients didn't even use levels. The system punished
					engagement without explanation.
				</div>
			</div>
			<div class="insight-card" data-num="insight 02">
				<div class="insight-title">Filtering friction</div>
				<div class="insight-body">
					Clunky time filters with confusing labels ("Last Semester," "This Semester"). No custom
					date range. Power users were manipulating URL parameters to get the data they needed.
				</div>
			</div>
			<div class="insight-card" data-num="insight 03">
				<div class="insight-title">Buried privacy controls</div>
				<div class="insight-body">
					An opt-out existed, but it was so deep in settings that some students who didn't want to
					be ranked weren't aware they could opt out, leading to frustration and support tickets.
				</div>
			</div>
		</div>
		<blockquote class="pull-quote">
			"The confusion wasn't about missing documentation. It was a lack of utility."
		</blockquote>
		<p class="body-text">
			Alongside the user pain, the leaderboard ran on legacy Angular code. This created slow load
			times (2-5 seconds) and techincal debt: it was difficult to maintain and incompatible with the
			direction the rest of the product was heading.
		</p>
		<div class="case-img-wrap">
			<img
				src="/leaderboard-before-filter-1.jpg"
				alt="Screenshot of the original leaderboard design, showing a ranked list of students with their points and levels"
				class="case-img"
			/>
			<span class="case-img-caption">The original group filtering — before the rebuild.</span>
		</div>
		<div class="case-img-wrap">
			<img
				src="/leaderboard-before-filter-2.jpg"
				alt="Screenshot of the original leaderboard design, showing a ranked list of students with their points and levels"
				class="case-img"
			/>
			<span class="case-img-caption">The original time filtering — before the rebuild.</span>
		</div>
	</section>

	<!-- 02 DISCOVERY -->
	<section class="cs-section" id="discovery">
		<div class="section-eyebrow">
			<span class="eyebrow-num">02</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Discovery</span>
		</div>
		<h2>How I validated what<br />I suspected.</h2>
		<p class="body-text">
			I developed a multi-channel data collection strategy to go beyond anecdotal feedback and build
			confidence in what we were solving.
		</p>
		<div class="solution-list" style="margin-top: 28px;">
			<div class="solution-item">
				<div class="solution-num">①</div>
				<div>
					<div class="solution-title">In-app user surveys</div>
					<div class="solution-body">
						Surfaced friction points directly from students and admins while they were experiencing
						them — highest signal-to-noise ratio.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">②</div>
				<div>
					<div class="solution-title">Internal CS team interviews</div>
					<div class="solution-body">
						The Customer Success team had a front-row seat to client frustration. Their pattern
						recognition was invaluable for identifying systemic vs. edge-case problems.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">③</div>
				<div>
					<div class="solution-title">5 customer interviews</div>
					<div class="solution-body">
						Direct conversations with admin users at client schools revealed the levels insight:
						that most schools simply weren't building their programs around levels at all.
					</div>
				</div>
			</div>
		</div>
		<!-- <div class="img-placeholder short">
			<span class="placeholder-icon">⊞</span>
			<span class="placeholder-label">Affinity map / synthesis board from discovery</span>
		</div> -->
	</section>

	<!-- 03 SOLUTIONING -->
	<section class="cs-section" id="solutions">
		<div class="section-eyebrow">
			<span class="eyebrow-num">03</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Solutioning</span>
		</div>
		<h2>Four decisions that changed<br />the product.</h2>
		<div class="solution-list">
			<div class="solution-item">
				<div class="solution-num">1</div>
				<div>
					<div class="solution-title">The smoking gun: remove levels from ranking</div>
					<div class="solution-body">
						The boldest call. If levels don't hold weight in the minds of most users, they shouldn't
						hold weight in the calculation. The new leaderboard is based solely on total points.
						Simple. Legible. Honest.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">2</div>
				<div>
					<div class="solution-title">Filter drawer: consolidated controls</div>
					<div class="solution-body">
						All filters moved into a single side-panel. No more scattered dropdowns. Custom date
						range UI added, eliminating URL hacking entirely. Pre-set options rewritten in plain
						language and reflected frequently used options.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">3</div>
				<div>
					<div class="solution-title">The Podium Finish</div>
					<div class="solution-body">
						Top 3 students get a high-impact visual treatment. I designed a podium finish that's
						built for mobile and big campus screens alike. Adds real gamification energy and
						shareability.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">4</div>
				<div>
					<div class="solution-title">Points breakdown sidebar</div>
					<div class="solution-body">
						A sidebar showing how a student earned their total — broken down by competency. Nudges
						students toward skill growth rather than just chasing a leaderboard number.
					</div>
				</div>
			</div>
		</div>
		<div class="solution-gallery">
			<div class="gallery-main">
				<button
					class="gallery-arrow gallery-arrow--prev"
					on:click={() => {
						selectedIndex = (selectedIndex - 1 + solutionImages.length) % solutionImages.length;
						selectedSolution = solutionImages[selectedIndex].src;
						selectedCaption = solutionImages[selectedIndex].caption;
					}}
					aria-label="Previous image">←</button
				>

				<div class="case-img-wrap gallery-img-wrap">
					<img
						src={selectedSolution}
						alt="Selected leaderboard screen"
						class="case-img main-solution-img"
					/>
					<span class="case-img-caption">{selectedCaption}</span>
				</div>

				<button
					class="gallery-arrow gallery-arrow--next"
					on:click={() => {
						selectedIndex = (selectedIndex + 1) % solutionImages.length;
						selectedSolution = solutionImages[selectedIndex].src;
						selectedCaption = solutionImages[selectedIndex].caption;
					}}
					aria-label="Next image">→</button
				>
			</div>

			<div class="img-grid-3 solution-thumbs">
				{#each solutionImages as img, i}
					<button
						class="thumb-btn"
						class:active={selectedIndex === i}
						on:click={() => {
							selectedIndex = i;
							selectedSolution = img.src;
							selectedCaption = img.caption;
						}}
					>
						<img src={img.src} alt={img.caption} class="thumb-img" />
					</button>
				{/each}
			</div>
		</div>
	</section>

	<!-- 04 SHAPING -->
	<section class="cs-section" id="shaping">
		<div class="section-eyebrow">
			<span class="eyebrow-num">04</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Shaping</span>
		</div>
		<h2>Blue sky → real world.<br />Budget is a design constraint.</h2>
		<p class="body-text">
			After the initial design phase, I had to shape the project to fit reality: 4–6 weeks, 2–3
			sprints, 30-40 story points. That means hard choices on the effort/impact matrix. Not
			everything made it. The features that survived were the ones that directly addressed the three
			core pain points discovered in research.
		</p>
		<!-- <div class="img-placeholder medium">
			<span class="placeholder-icon">⬡</span>
			<span class="placeholder-label">Effort / impact matrix — shaping decisions</span>
		</div> -->
		<p class="body-text">
			Concessions were made. Features deferred. But the shape we landed on was clean, defensible,
			and buildable within the constraints we had.
		</p>
	</section>

	<!-- 05 OUTCOMES -->
	<section class="cs-section" id="outcomes">
		<div class="section-eyebrow">
			<span class="eyebrow-num">05</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Outcomes</span>
		</div>
		<h2>What changed.</h2>
		<div class="insight-grid">
			<div class="insight-card" data-num="">
				<div class="insight-title">30%</div>
				<div class="insight-body">Target satisfaction improvement (from 60% baseline)</div>
			</div>
			<div class="insight-card" data-num="">
				<div class="insight-title">&lt;1s</div>
				<div class="insight-body">Target load time (down from 2-5 seconds)</div>
			</div>
			<div class="insight-card" data-num="">
				<div class="insight-title">0</div>
				<div class="insight-body">Angular code remaining — fully migrated to React</div>
			</div>
		</div>

		<p class="body-text">
			Beyond the metrics the filter drawer component became a reusable pattern applied across the
			rest of the app. The leaderboard went from a feature clients complained about to one they
			actively showcased on campus screens, in newsletters, and on social media.
		</p>
		<p class="body-text" style="margin-top: 16px;">
			The podium lives on large displays in campus buildings. That visibility was always the point.
			Now the design matches it.
		</p>
		<div class="case-img-wrap">
			<video src="/leaderboard-final-video.mov" class="case-img" autoplay loop muted playsinline
			></video>
			<span class="case-img-caption">The redesigned leaderboard — delivered product.</span>
		</div>
	</section>
</div>

<!-- ─── NEXT PROJECT ─── -->
<ViewAllWork />

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
		--light-stone: #ede8df;
	}

	:global(html) {
		scroll-behavior: smooth;
	}

	:global(body) {
		background: var(--warm-white);
		font-family: 'Lora', Georgia, serif;
		color: var(--ink);
		overflow-x: hidden;
	}

	/* ─── GRAIN ─── */
	.grain {
		position: fixed;
		inset: 0;
		pointer-events: none;
		z-index: 200;
		opacity: 0.025;
		background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
		background-size: 180px;
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
		border-radius: 0 2px 2px 0;
		transition: width 0.1s linear;
	}

	/* ─── NAV ─── */
	.top-nav {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 90;
		padding: 20px 48px;
		display: flex;
		align-items: center;
		justify-content: space-between;
		background: linear-gradient(to bottom, var(--warm-white) 60%, transparent);
	}

	.nav-back {
		font-family: 'Caveat', cursive;
		font-size: 17px;
		color: var(--stone);
		text-decoration: none;
		display: flex;
		align-items: center;
		gap: 8px;
		transition: color 0.2s;
	}
	.nav-back:hover {
		color: var(--clay);
	}
	.nav-back::before {
		content: '←';
	}

	.nav-name {
		font-family: 'Caveat', cursive;
		font-size: 17px;
		color: var(--clay);
	}

	/* ─── HERO ─── */
	.case-hero {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: flex-end;
		padding: 0 0 80px;
		position: relative;
		overflow: hidden;
	}

	.hero-bg-text {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		font-family: 'Caveat', cursive;
		font-size: clamp(100px, 18vw, 200px);
		font-weight: 600;
		color: var(--light-stone);
		white-space: nowrap;
		pointer-events: none;
		letter-spacing: -4px;
		user-select: none;
		opacity: 0.7;
	}

	.hero-content {
		max-width: 860px;
		margin: 0 auto;
		padding: 0 48px;
		position: relative;
		z-index: 2;
	}

	.case-tag {
		display: inline-flex;
		gap: 8px;
		margin-bottom: 24px;
		flex-wrap: wrap;
	}

	.tag-pill {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		padding: 5px 14px;
		border-radius: 100px;
		border: 1.5px solid;
		letter-spacing: 0.3px;
	}
	.tag-pill.pm {
		border-color: var(--moss);
		color: var(--moss);
	}
	.tag-pill.ux {
		border-color: var(--clay);
		color: var(--clay);
	}
	.tag-pill.dev {
		border-color: var(--bark);
		color: var(--bark);
	}

	.case-hero h1 {
		font-size: clamp(42px, 7vw, 72px);
		font-weight: 400;
		line-height: 1.1;
		letter-spacing: -2px;
		margin-bottom: 20px;
		opacity: 0;
		transform: translateY(30px);
		animation: fadeUp 0.9s ease forwards 0.2s;
	}

	.subtitle {
		font-size: 18px;
		color: var(--stone);
		font-style: italic;
		line-height: 1.6;
		max-width: 560px;
		opacity: 0;
		transform: translateY(20px);
		animation: fadeUp 0.9s ease forwards 0.4s;
	}

	@keyframes fadeUp {
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	/* ─── META STRIP ─── */
	.meta-strip {
		background: var(--ink);
		padding: 40px 0;
	}

	.meta-inner {
		max-width: 860px;
		margin: 0 auto;
		padding: 0 48px;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 32px;
	}

	.meta-label {
		font-family: 'Caveat', cursive;
		font-size: 13px;
		color: var(--sage);
		letter-spacing: 1.5px;
		text-transform: uppercase;
		margin-bottom: 6px;
	}

	.meta-value {
		font-size: 15px;
		color: var(--sand);
		line-height: 1.5;
	}

	/* ─── CASE BODY ─── */
	.case-body {
		max-width: 860px;
		margin: 0 auto;
		padding: 0 48px;
	}

	/* ─── SECTIONS ─── */
	.cs-section {
		padding: 80px 0;
		border-bottom: 1px solid var(--light-stone);
		opacity: 0;
		transform: translateY(32px);
		transition:
			opacity 0.8s ease,
			transform 0.8s ease;
	}

	:global(.cs-section.visible) {
		opacity: 1;
		transform: translateY(0);
	}

	.cs-section:last-child {
		border-bottom: none;
	}

	.section-eyebrow {
		display: flex;
		align-items: center;
		gap: 12px;
		margin-bottom: 20px;
	}

	.eyebrow-num {
		font-family: 'Caveat', cursive;
		font-size: 13px;
		color: var(--clay);
		letter-spacing: 1px;
	}

	.eyebrow-line {
		flex: 1;
		max-width: 40px;
		height: 1px;
		background: var(--clay);
		opacity: 0.5;
	}

	.eyebrow-label {
		font-family: 'Caveat', cursive;
		font-size: 15px;
		color: var(--clay);
		letter-spacing: 1.5px;
		text-transform: uppercase;
	}

	.cs-section h2 {
		font-size: clamp(28px, 4vw, 42px);
		font-weight: 400;
		line-height: 1.2;
		letter-spacing: -0.5px;
		margin-bottom: 28px;
	}

	.body-text {
		font-size: 17px;
		line-height: 1.85;
		color: #4a4440;
	}

	.body-text + .body-text {
		margin-top: 16px;
	}

	/* ─── HAND-DRAWN UNDERLINE ─── */
	.hand-underline {
		position: relative;
		display: inline;
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

	/* ─── IMAGE PLACEHOLDERS ─── */
	.img-placeholder {
		width: 100%;
		background: var(--light-stone);
		border-radius: 8px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 10px;
		margin: 36px 0;
		border: 1.5px dashed var(--clay);
		opacity: 0.7;
		position: relative;
		overflow: hidden;
	}
	.img-placeholder::before {
		content: '';
		position: absolute;
		inset: 0;
		background: repeating-linear-gradient(
			45deg,
			transparent,
			transparent 12px,
			rgba(196, 149, 106, 0.06) 12px,
			rgba(196, 149, 106, 0.06) 13px
		);
	}
	.img-placeholder.tall {
		height: 400px;
	}
	.img-placeholder.medium {
		height: 280px;
	}
	.img-placeholder.short {
		height: 200px;
	}

	.placeholder-icon {
		font-family: 'Caveat', cursive;
		font-size: 32px;
		color: var(--clay);
		opacity: 0.6;
		position: relative;
		z-index: 1;
	}

	.placeholder-label {
		font-family: 'Caveat', cursive;
		font-size: 15px;
		color: var(--bark);
		opacity: 0.7;
		position: relative;
		z-index: 1;
		text-align: center;
		padding: 0 20px;
	}

	.img-grid-2 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 16px;
		margin: 36px 0;
	}

	.img-grid-3 {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		gap: 14px;
		margin: 36px 0;
	}

	/* ─── PULL QUOTE ─── */
	.pull-quote {
		font-size: clamp(20px, 3vw, 26px);
		font-style: italic;
		line-height: 1.55;
		color: var(--clay);
		border-left: 3px solid var(--clay);
		padding: 4px 0 4px 28px;
		margin: 36px 0;
	}

	/* ─── INSIGHT CARDS ─── */
	.insight-grid {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		gap: 16px;
		margin: 32px 0;
	}

	.insight-card {
		padding: 24px;
		border: 1.5px solid var(--light-stone);
		border-radius: 6px;
		background: var(--cream);
		position: relative;
		transition: transform 0.25s ease;
	}
	.insight-card:hover {
		transform: translateY(-3px);
	}
	.insight-card::before {
		content: attr(data-num);
		position: absolute;
		top: -14px;
		left: 20px;
		font-family: 'Caveat', cursive;
		font-size: 13px;
		background: var(--cream);
		color: var(--clay);
		padding: 0 6px;
		border: 1.5px solid var(--clay);
		border-radius: 100px;
	}

	.insight-title {
		font-size: 15px;
		font-weight: 500;
		margin-bottom: 10px;
		line-height: 1.3;
	}

	.insight-body {
		font-size: 14px;
		line-height: 1.7;
		color: var(--stone);
	}

	/* ─── SOLUTION LIST ─── */
	.solution-list {
		display: flex;
		flex-direction: column;
		gap: 20px;
		margin: 32px 0;
	}

	.solution-item {
		display: grid;
		grid-template-columns: 48px 1fr;
		gap: 20px;
		align-items: start;
		padding: 24px;
		background: var(--cream);
		border-radius: 6px;
		border: 1.5px solid var(--light-stone);
		transition: transform 0.25s ease;
	}
	.solution-item:hover {
		transform: translateX(4px);
	}

	.solution-num {
		font-family: 'Caveat', cursive;
		font-size: 36px;
		color: var(--clay);
		opacity: 0.5;
		line-height: 1;
		text-align: center;
	}

	.solution-title {
		font-size: 16px;
		font-weight: 500;
		margin-bottom: 8px;
	}

	.solution-body {
		font-size: 15px;
		line-height: 1.75;
		color: #4a4440;
	}

	/* ─── KPI BAND ─── */
	.kpi-band {
		background: var(--ink);
		border-radius: 8px;
		padding: 40px;
		margin: 48px 0;
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 32px;
	}

	.kpi-item {
		text-align: center;
	}

	.kpi-num {
		font-size: clamp(36px, 5vw, 52px);
		font-weight: 400;
		color: var(--clay);
		line-height: 1;
		margin-bottom: 8px;
		font-family: 'Lora', serif;
	}

	.kpi-label {
		font-family: 'Caveat', cursive;
		font-size: 15px;
		color: var(--sage);
		line-height: 1.4;
		letter-spacing: 0.5px;
	}

	.kpi-divider {
		width: 1px;
		background: rgba(255, 255, 255, 0.1);
		align-self: stretch;
	}

	/* ─── NEXT PROJECT ─── */
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

	/* ─── RESPONSIVE ─── */
	@media (max-width: 700px) {
		.top-nav {
			padding: 16px 20px;
		}
		.hero-content,
		.case-body {
			padding: 0 20px;
		}
		.meta-inner {
			grid-template-columns: 1fr 1fr;
			padding: 0 20px;
		}
		.insight-grid {
			grid-template-columns: 1fr;
		}
		.img-grid-2,
		.img-grid-3 {
			grid-template-columns: 1fr;
		}
		.kpi-band {
			grid-template-columns: 1fr;
			padding: 28px;
		}
		.kpi-divider {
			display: none;
		}
		.next-project {
			padding: 60px 20px;
		}
	}

	.case-img-wrap {
		margin: 36px 0;
		display: flex;
		flex-direction: column;
		gap: 10px;
	}

	.case-img {
		width: 100%;
		border-radius: 8px;
		display: block;
		border: 1.5px solid var(--light-stone);
	}

	.case-img-caption {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		color: var(--stone);
		text-align: center;
		letter-spacing: 0.3px;
	}

	/* ─── SOLUTION IMAGE GALLERY ─── */
	.main-solution-img {
		transition: opacity 0.2s ease;
	}

	.solution-thumbs {
		margin-top: 12px;
	}

	.thumb-btn {
		display: block;
		width: 100%;
		padding: 0;
		background: none;
		border: 2px solid transparent;
		border-radius: 8px;
		cursor: pointer;
		overflow: hidden;
		transition:
			border-color 0.2s ease,
			transform 0.2s ease;
	}

	.thumb-btn:hover {
		transform: translateY(-2px);
		border-color: var(--stone);
	}

	.thumb-btn.active {
		border-color: var(--clay);
	}

	.thumb-img {
		width: 100%;
		display: block;
		border-radius: 6px;
		opacity: 0.7;
		transition: opacity 0.2s ease;
	}

	.thumb-btn.active .thumb-img,
	.thumb-btn:hover .thumb-img {
		opacity: 1;
	}

	/* ─── GALLERY ARROWS ─── */
	.solution-gallery {
		margin: 36px 0;
	}

	.gallery-main {
		display: grid;
		grid-template-columns: 40px 1fr 40px;
		align-items: center;
		gap: 12px;
	}

	.gallery-img-wrap {
		margin: 0;
	}

	.gallery-arrow {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 36px;
		height: 36px;
		border-radius: 50%;
		border: 1.5px solid var(--light-stone);
		background: var(--cream);
		font-family: 'Caveat', cursive;
		font-size: 18px;
		color: var(--stone);
		cursor: pointer;
		transition: all 0.2s ease;
		flex-shrink: 0;
		align-self: center;
	}

	.gallery-arrow:hover {
		border-color: var(--clay);
		color: var(--clay);
		transform: scale(1.1);
	}

	.solution-thumbs {
		margin-top: 12px;
	}

	@media (max-width: 700px) {
		.gallery-main {
			grid-template-columns: 32px 1fr 32px;
			gap: 8px;
		}
		.gallery-arrow {
			width: 28px;
			height: 28px;
			font-size: 14px;
		}
	}
</style>
