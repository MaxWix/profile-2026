<script>
	import { onMount } from 'svelte';

	const solutionImages = [
		{ src: '/kims/kimsPersona1.jpg' },
		{ src: '/kims/kimsPersona2.jpg' },
		{ src: '/kims/kimsPersona3.jpg' }
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
	<title>Kim's Dragon — Max's Portfolio</title>
</svelte:head>

<div class="grain"></div>
<div class="progress-bar" id="progress"></div>

<nav class="top-nav">
	<a href="/" class="nav-back">back to work</a>
	<span class="nav-name">Max</span>
</nav>

<!-- ─── HERO ─── -->
<header class="case-hero">
	<div class="hero-bg-text">Kim's Dragon</div>
	<div class="hero-content">
		<div class="case-tag">
			<span class="tag-pill ux">UX / UI Design</span>
			<span class="tag-pill research">UX Research</span>
		</div>
		<h1>Kim's Dragon<br /><em>Mobile Ordering</em></h1>
		<p class="subtitle">
			A mobile take-out app for a beloved campus food truck — designing for familiarity,
			personality, and a line that moves faster.
		</p>
	</div>
</header>

<!-- ─── META STRIP ─── -->
<div class="meta-strip">
	<div class="meta-inner">
		<div class="meta-item">
			<div class="meta-label">Client</div>
			<div class="meta-value">Kim's Dragon Food Truck</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">Timeline</div>
			<div class="meta-value">11 weeks</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">My Role</div>
			<div class="meta-value">UX Design & Research</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">Output</div>
			<div class="meta-value">High-fidelity prototype</div>
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
		<h2>A food truck worth<br />waiting in line for —<br />until you don't have to.</h2>
		<p class="body-text">
			Behind Drexel University's Main Building, a long line of food trucks serve West Philadelphia.
			Kim's Dragon stands out with its diverse and delicious Asian cuisine, attracting a mix of
			college students and locals. Our team — captivated by the truck's food and friendly staff —
			set out to design a mobile take-out app.
		</p>
		<p class="body-text">
			Our goal went beyond making the ordering process efficient. We wanted to capture the vibrant
			personality of Kim's Dragon within the app, seamlessly extending the culinary experience
			customers already loved.
		</p>

		<div class="case-img-wrap">
			<img src="/kims/kimsGoals.jpg" alt="Kims Dragon Project Goals" class="case-img" />
		</div>
	</section>

	<!-- 01 CHALLENGE -->
	<section class="cs-section" id="challenge">
		<div class="section-eyebrow">
			<span class="eyebrow-num">01</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">The Challenge</span>
		</div>
		<h2>Late to digital.<br />Long on <span class="hand-underline">lines</span>.</h2>
		<p class="body-text">
			Kim's Dragon had no digital ordering solution. The lines were long — sometimes insufferable.
			Our main challenge was to offer a solution that helped customers skip the wait while helping
			Kim's Dragon adapt to an unavoidable digital age.
		</p>
		<p class="body-text">
			We had 11 weeks to deliver a final prototype. The constraint shaped every decision.
		</p>

		<div class="insight-grid">
			<div class="insight-card" data-num="challenge 01">
				<div class="insight-title">Long wait times</div>
				<div class="insight-body">
					Lines at Kim's Dragon were a consistent pain point for the time-constrained college
					students and workers who made up their customer base.
				</div>
			</div>
			<div class="insight-card" data-num="challenge 02">
				<div class="insight-title">No digital presence</div>
				<div class="insight-body">
					No app, no online ordering, no way to plan ahead. The entire experience was in-person
					only, leaving efficiency-seeking customers underserved.
				</div>
			</div>
			<div class="insight-card" data-num="challenge 03">
				<div class="insight-title">Personality at risk</div>
				<div class="insight-body">
					Any digital solution risked making Kim's Dragon feel generic — like a restaurant page
					inside Uber Eats rather than a place with its own identity.
				</div>
			</div>
		</div>
	</section>

	<!-- 02 RESEARCH -->
	<section class="cs-section" id="research">
		<div class="section-eyebrow">
			<span class="eyebrow-num">02</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Research</span>
		</div>
		<h2>Observational testing<br />and field interviews.</h2>
		<p class="body-text">
			Our first point of action was observational testing and field interviews at Kim's Dragon —
			understanding who actually uses this truck and what their ordering experience looks like in
			the real world.
		</p>
		<p class="body-text">
			From several days of fieldwork we developed three distinct user personas representing the
			range of people who order from Kim's Dragon: the time-pressed student, the regular lunch-hour
			worker, and the casual walk-up customer.
		</p>

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

		<p class="body-text">
			We also mapped a user journey for Sarah Parker — a composite of our most time-constrained
			persona — tracking her emotions and actions through the full ordering experience. This
			illuminated exactly where frustration peaked and where a mobile solution could intervene.
		</p>

		<div class="case-img-wrap">
			<img
				src="/kims/userJourney.png"
				alt="Sarah Parker user journey map, showing her emotions and actions throughout the ordering process at Kim's Dragon"
				class="case-img"
			/>
		</div>
	</section>

	<!-- 03 LOW-FI -->
	<section class="cs-section" id="lofi">
		<div class="section-eyebrow">
			<span class="eyebrow-num">03</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Low Fidelity</span>
		</div>
		<h2>Design for familiarity<br />first.</h2>
		<p class="body-text">
			Taking inspiration from existing food ordering apps, we sketched initial screen concepts
			before moving into low-fi prototypes. Our guiding tension: create something outstanding, but
			also something anyone could pick up and use immediately.
		</p>
		<p class="body-text">
			We built out prototypes for each step of ordering the Sesame Chicken — a task specific enough
			to create a real testing environment.
		</p>

		<div class="case-img-wrap">
			<img
				src="/kims/lowFiProto.jpg"
				alt="Screenshots of the low-fidelity prototype"
				class="case-img"
			/>
			<span class="case-img-caption">Low Fidelity Prototype</span>
		</div>

		<div class="section-sub-label">Testing takeaways</div>
		<div class="solution-list">
			<div class="solution-item">
				<div class="solution-num">①</div>
				<div>
					<div class="solution-title">Familiarity validated</div>
					<div class="solution-body">
						Most users' first reaction was that the prototype felt familiar to other food ordering
						apps — a strong signal we were heading in the right direction.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">②</div>
				<div>
					<div class="solution-title">"View All" confused users</div>
					<div class="solution-body">
						The copy wasn't clear enough — users weren't sure it would lead to the full menu. Label
						needed to be updated to make the action explicit.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">③</div>
				<div>
					<div class="solution-title">Queue status needed clearer descriptors</div>
					<div class="solution-body">
						"Busy" under Current Queue Status didn't tell users enough. Each status option needed
						better language to actually set expectations.
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- 04 MID-FI -->
	<section class="cs-section" id="midfi">
		<div class="section-eyebrow">
			<span class="eyebrow-num">04</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Mid Fidelity</span>
		</div>
		<h2>Color, imagery,<br />and new friction.</h2>
		<p class="body-text">
			With low-fi feedback in hand, we upgraded to mid-fidelity — adding color, images, and
			iconography. This was when the harder design problems started to surface.
		</p>

		<div class="case-img-wrap">
			<img
				src="/kims/midFiProto.jpg"
				alt="Screenshots of the mid-fidelity prototype"
				class="case-img"
			/>
			<span class="case-img-caption">Mid Fidelity Prototype</span>
		</div>

		<div class="section-sub-label">Testing takeaways</div>
		<div class="solution-list">
			<div class="solution-item">
				<div class="solution-num">①</div>
				<div>
					<div class="solution-title">The app felt generic</div>
					<div class="solution-body">
						Users felt they were inside a restaurant page of a larger app like Uber Eats, not Kim's
						Dragon's own app. We needed to make the brand identity much more present throughout.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">②</div>
				<div>
					<div class="solution-title">Icon color contrast was insufficient</div>
					<div class="solution-body">
						The yellow and blue of our menu category icons didn't have enough contrast. We needed to
						reassess the palette to bring more clarity.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">③</div>
				<div>
					<div class="solution-title">Checkout progress was invisible</div>
					<div class="solution-body">
						Users couldn't tell where they were in the multi-page checkout process. We added a
						progress bar to the top of checkout pages so users could orient themselves and navigate
						freely.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">④</div>
				<div>
					<div class="solution-title">No order status after placing</div>
					<div class="solution-body">
						Once an order was placed and the user returned to the menu, there was no indication
						anything had happened. We added an anchored status banner to the top of the home page so
						the order was always a tap away.
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- 05 HI-FI -->
	<section class="cs-section" id="hifi">
		<div class="section-eyebrow">
			<span class="eyebrow-num">05</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">High Fidelity</span>
		</div>
		<h2>All we learned,<br />made real.</h2>
		<p class="body-text">
			Incorporating everything from two rounds of testing, we built our high-fidelity prototype. One
			key addition: a third color — hot pink — introduced specifically to signal important functions
			and guide users through critical moments.
		</p>

		<div class="case-img-wrap">
			<img
				src="/kims/hiFiProto.jpg"
				alt="Screenshots of the high-fidelity prototype"
				class="case-img"
			/>
			<span class="case-img-caption">High Fidelity Prototype</span>
		</div>

		<div class="section-sub-label">Final testing takeaways</div>
		<div class="solution-list">
			<div class="solution-item">
				<div class="solution-num">✓</div>
				<div>
					<div class="solution-title">Core tasks were intuitive</div>
					<div class="solution-body">
						Resoundingly positive feedback — none of our testers struggled to find their way around.
						Ordering felt familiar and easy.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">↻</div>
				<div>
					<div class="solution-title">Progress bar needed clearer states</div>
					<div class="solution-body">
						Users still struggled to distinguish past, present, and future steps in the checkout
						progress bar. A final color update resolved this — establishing clear visual states for
						where you've been, where you are, and what's ahead.
					</div>
				</div>
			</div>
		</div>

		<div class="prototype-cta">
			<a
				href="https://www.figma.com/proto/Hswy8UGayaGxxAgiDJoCCk/IDM215-PROTEAM-COPY?page-id=1562%3A9000&type=design&node-id=1562-10688&viewport=399%2C307%2C0.13&t=QR7GDKQ8MXTRooFF-1&scaling=min-zoom&starting-point-node-id=1562%3A10937&mode=design"
				target="_blank"
				class="proto-btn"
			>
				View prototype in Figma →
			</a>
		</div>
	</section>

	<!-- 06 RESULTS -->
	<section class="cs-section" id="results">
		<div class="section-eyebrow">
			<span class="eyebrow-num">06</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Results & Reflections</span>
		</div>
		<h2>What we built.<br />What we learned.</h2>
		<p class="body-text">
			Throughout the testing process, when asking participants if this app would be easier than
			ordering in person, confidence grew consistently week over week. Two features stood out as
			particularly valuable to Kim's Dragon's customer base.
		</p>

		<div class="insight-grid" style="margin-top: 32px;">
			<div class="insight-card" data-num="feature 01">
				<div class="insight-title">Live queue status</div>
				<div class="insight-body">
					Real-time and estimated wait times — informed by current order volume and time of day —
					gave customers the context they needed to decide when and whether to order.
				</div>
			</div>
			<div class="insight-card" data-num="feature 02">
				<div class="insight-title">Order ahead</div>
				<div class="insight-body">
					The core value proposition. Users with tight schedules could order ahead and pick up
					without ever joining the line — a genuine improvement over the existing experience.
				</div>
			</div>
			<div class="insight-card" data-num="lesson">
				<div class="insight-title">Details are never small</div>
				<div class="insight-body">
					A slightly off button height. A less-than-smooth page transition. Users noticed — and
					those details became more memorable than the parts they enjoyed. Good design is what's
					absent from the conversation.
				</div>
			</div>
		</div>

		<blockquote class="pull-quote">
			"Balancing familiar patterns with a personality unique to the restaurant was our hardest
			design challenge — and our most important one."
		</blockquote>

		<p class="body-text">
			This project taught us that mental models and personality aren't in conflict — but you have to
			earn the personality by getting the fundamentals right first. By the end of the term, we had
			both.
		</p>
	</section>
</div>

<!-- ─── NEXT PROJECT ─── -->
<div class="next-project">
	<div class="next-label">next case study</div>
	<h2>What else has Max built?</h2>
	<a href="/" class="next-btn">View all work →</a>
</div>

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

	.grain {
		position: fixed;
		inset: 0;
		pointer-events: none;
		z-index: 200;
		opacity: 0.025;
		background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
		background-size: 180px;
	}

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
		font-size: clamp(100px, 20vw, 220px);
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
	.tag-pill.research {
		border-color: var(--stone);
		color: var(--stone);
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

	/* ─── META ─── */
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

	/* ─── BODY ─── */
	.case-body {
		max-width: 860px;
		margin: 0 auto;
		padding: 0 48px;
	}

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

	.section-sub-label {
		font-family: 'Caveat', cursive;
		font-size: 15px;
		color: var(--moss);
		letter-spacing: 1px;
		text-transform: uppercase;
		margin: 36px 0 0;
		display: flex;
		align-items: center;
		gap: 10px;
	}
	.section-sub-label::before {
		content: '';
		display: inline-block;
		width: 20px;
		height: 1px;
		background: var(--moss);
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
		gap: 16px;
		margin: 20px 0 0;
	}

	.solution-item {
		display: grid;
		grid-template-columns: 48px 1fr;
		gap: 20px;
		align-items: start;
		padding: 22px 24px;
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
		font-size: 28px;
		color: var(--clay);
		opacity: 0.5;
		line-height: 1.2;
		text-align: center;
		padding-top: 2px;
	}

	.solution-title {
		font-size: 16px;
		font-weight: 500;
		margin-bottom: 6px;
	}
	.solution-body {
		font-size: 15px;
		line-height: 1.75;
		color: #4a4440;
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

	/* ─── PROTOTYPE CTA ─── */
	.prototype-cta {
		margin: 40px 0 0;
		display: flex;
	}

	.proto-btn {
		font-family: 'Caveat', cursive;
		font-size: 18px;
		color: var(--bark);
		border: 1.5px solid var(--bark);
		padding: 12px 28px;
		border-radius: 100px;
		text-decoration: none;
		transition: all 0.25s ease;
		background: transparent;
	}
	.proto-btn:hover {
		background: var(--bark);
		color: var(--warm-white);
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
		height: 420px;
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
		.next-project {
			padding: 60px 20px;
		}
	}

	.case-img-wrap {
		margin: 36px 0;
		display: flex;
		flex-direction: column;
		gap: 10px;
		max-height: 600px;
		overflow: hidden;
		border-radius: 8px;
	}

	.case-img {
		width: 100%;
		border-radius: 8px;
		display: block;
		border: 1.5px solid var(--light-stone);
		object-fit: cover;
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

	.img-grid-3 {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		gap: 14px;
		margin: 36px 0;
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
