<script>
	import { onMount } from 'svelte';
	import BackToWork from '$lib/components/BackToWork.svelte';
	import ViewAllWork from '$lib/components/ViewAllWork.svelte';

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
	<title>Loam — Max's Portfolio</title>
</svelte:head>

<div class="grain"></div>
<div class="progress-bar" id="progress"></div>

<nav class="top-nav">
	<BackToWork />
	<span class="nav-name">Max Wix</span>
</nav>

<!-- ─── HERO ─── -->
<header class="case-hero">
	<div class="hero-bg-text">Loam</div>
	<div class="hero-content">
		<div class="case-tag">
			<span class="tag-pill pm">Product Management</span>
			<span class="tag-pill ux">UX / UI Design</span>
			<span class="tag-pill dev">Front-End Engineering</span>
			<span class="tag-pill research">UX Research</span>
		</div>
		<h1>Loam</h1>
		<p class="subtitle">
			This isn't a case study about driving revenue or fueling engagement. It's about defining a
			strict, value driven mission — and solving a problem that the majority of our population
			faces, myself included.
		</p>
	</div>
</header>

<!-- ─── META STRIP ─── -->
<div class="meta-strip">
	<div class="meta-inner">
		<div class="meta-item">
			<div class="meta-label">Type</div>
			<div class="meta-value">Senior Capstone Project</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">Timeline</div>
			<div class="meta-value">10 months</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">My Role</div>
			<div class="meta-value">Project Lead & PM</div>
		</div>
		<div class="meta-item">
			<div class="meta-label">Team</div>
			<div class="meta-value">7 people</div>
		</div>
	</div>
</div>

<div class="case-body">
	<!-- 00 ORIGIN -->
	<section class="cs-section" id="origin">
		<div class="section-eyebrow">
			<span class="eyebrow-num">00</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Origin</span>
		</div>
		<h2>My proudest work.<br />Built with seven people who<br />believed in it from day one.</h2>
		<div class="case-img-wrap">
			<img src="/loam-product-screens.jpg" alt="loam product screens" class="case-img" />
		</div>
		<p class="body-text">
			In the summer of 2026 I pitched Loam to six fellow students in my major. I feel incredibly
			grateful to have found a team completely aligned with me in our goals and values from day one.
		</p>

		<div class="team-grid">
			<div class="team-item">
				<div class="team-name">Chem Duong</div>
				<div class="team-role">Lead UI & Product Designer</div>
			</div>
			<div class="team-item">
				<div class="team-name">Dom Scott</div>
				<div class="team-role">UX Designer</div>
			</div>
			<div class="team-item">
				<div class="team-name">Ella Fitzgerald</div>
				<div class="team-role">Lead Developer</div>
			</div>
			<div class="team-item">
				<div class="team-name">Enoch Tuffour</div>
				<div class="team-role">UI & Brand Designer</div>
			</div>
			<div class="team-item">
				<div class="team-name">Gavin Cochrane</div>
				<div class="team-role">UX Researcher</div>
			</div>
			<div class="team-item">
				<div class="team-name">Joe Chindemi</div>
				<div class="team-role">UX Designer</div>
			</div>
			<div class="team-item team-item--me">
				<div class="team-name">Max Wix</div>
				<div class="team-role">Product Manager</div>
			</div>
		</div>

		<p class="body-text" style="margin-top: 28px;">
			As PM and team lead I wore many hats: developing and revising our roadmap across 10 months,
			shepherding Loam's ethos through every decision, distributing work across the team,
			contributing to designs, and working directly with our lead developer to build the web-app.
		</p>
		<p class="body-text" style="margin-top: 28px;">
			In addition to my contributions building the platform, I was responsible for managing our
			relationships and feedback loops with our users, establishing the brand voice, writing our
			copy, and coordinating community events.
		</p>
		<div class="case-img-wrap">
			<img src="/loam-roadmap.png" alt="loam product screens" class="case-img" />
			<span class="case-img-caption">Project Roadmap</span>
		</div>
	</section>

	<!-- 01 PROBLEM -->
	<section class="cs-section" id="problem">
		<div class="section-eyebrow">
			<span class="eyebrow-num">01</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">The Problem</span>
		</div>
		<h2>
			Meaningful connection has been<br />sacrificed for
			<span class="hand-underline">engagement</span>.
		</h2>
		<p class="body-text">
			Social media platforms are driven by design that prioritizes virality, controversy, and
			superficial metrics. This environment has created unhealthy consumption habits and
			incentivizes posting content designed to capture attention rather than share and connect.
		</p>
		<p class="body-text">
			Beyond individual well-being, the pervasive nature of these platforms has broader societal
			consequences. They've become breeding grounds for misinformation, eroding public trust and
			building social echo-chambers that dramatically increase polarization between social groups
			and undermine democratic institutions.
		</p>

		<p class="body-text">
			As the dominant players remain focused on this "addiction race," there is a clear opportunity
			for a new kind of social network: one that is designed for intentional connection with those
			we care about.
		</p>

		<blockquote class="pull-quote">
			"It's a constant pursuit of hijacking my brain to keep me on the app as long as possible."
		</blockquote>
		<p class="body-text">
			We validated this tension through extensive secondary research, surveying a combined 108
			participants, and completing dozens of guerrilla interviews in public parks in Philadelphia
			and around Drexel's campus. The appetite for something better was real.
		</p>
		<div class="case-img-wrap">
			<img
				src="/loam-social-media-survey.png"
				alt="Screenshot of the original leaderboard design, showing a ranked list of students with their points and levels"
				class="case-img"
			/>
			<span class="case-img-caption">54 participants surveyed for a feeler-survey</span>
		</div>
		<div class="case-img-wrap">
			<img
				src="/loam-guerilla-interview-quotes.png"
				alt="Screenshot of the original leaderboard design, showing a ranked list of students with their points and levels"
				class="case-img"
			/>
			<span class="case-img-caption">Direct quotes from our on-the-street interviews</span>
		</div>
		<div class="insight-grid">
			<div class="insight-card" data-num="finding 01">
				<div class="insight-title">People feel disconnected</div>
				<div class="insight-body">
					Social media shows users posts from people they barely know or care about. Drowning in
					algorithmically curated content, feeds covered with "suggested" posts and ads, they are
					frustrated by lack of authenticity and simplicity.
				</div>
			</div>
			<div class="insight-card" data-num="finding 02">
				<div class="insight-title">It's not all bad</div>
				<div class="insight-body">
					People still believe that social media does help them keep connected to people that
					matter. They like and want to be able to keep up with friends, share moments, and stay
					updated on interests and hobbies.
				</div>
			</div>
			<div class="insight-card" data-num="finding 03">
				<div class="insight-title">A clear tension</div>
				<div class="insight-body">
					People value the connection that social media enables, but are frustrated by the platform
					behaviors designed to exploit that value. <b
						>There is a clear need for social media to be a tool for connection, learning, and
						inspiration without the noise.</b
					>
				</div>
			</div>
		</div>
	</section>

	<!-- 02 WHAT IS LOAM -->
	<section class="cs-section" id="what">
		<div class="section-eyebrow">
			<span class="eyebrow-num">02</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">What is Loam</span>
		</div>
		<h2>A social app built for<br />connection, not consumption.</h2>
		<p class="body-text">
			Loam is a social sharing app that has created an ideal foundation for growing and maintaining
			meaningful relationships. Our designs are algorithm and metric free, working to help users
			share authentically.
		</p>
		<p class="body-text">
			Each feature — or deliberate lack thereof — is built to foster healthy online social habits
			and eschew the dark patterns present on existing platforms. Our commitment is to the
			betterment of each user: not their data, not their attention, not their profitability.
		</p>
		<p class="body-text">
			We had to unlearn much of what we knew about building social platforms and redefine what good
			design truly means. The guiding question for every decision we made:
		</p>

		<blockquote class="pull-quote">
			"How can we effectively incorporate ethical consideration into each decision we make while
			designing and building Loam?"
		</blockquote>

		<p class="body-text">
			Our first order of business was developing our values and mission. What loam should be and
			what loam shouldn't be for our users. Every design, development, social media, and copy
			decision we made was put up against these values as we went.
		</p>
	</section>

	<!-- 03 BRANDING -->
	<section class="cs-section" id="branding">
		<div class="section-eyebrow">
			<span class="eyebrow-num">03</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Branding</span>
		</div>
		<h2>Establishing an identity that<br />feels like the product.</h2>
		<p class="body-text">
			We conducted a desirability study to understand how potential users emotionally responded to
			our idea. The results directly informed the look, feel, and values of the brand.
		</p>

		<div class="case-img-wrap">
			<img
				src="/loam-desirability-2.png"
				alt="Screenshot of the original leaderboard design, showing a ranked list of students with their points and levels"
				class="case-img"
			/>
			<span class="case-img-caption"
				>Most users thought of natural imagery when visualizing connection</span
			>
		</div>
		<div class="case-img-wrap">
			<img src="/loam-desirability-1.png" alt="" class="case-img" />
			<span class="case-img-caption"
				>When user's think of loam, they think of Organic qualities that inspire Growth and Warmth</span
			>
		</div>
		<div class="insight-grid">
			<div class="insight-card" data-num="72%">
				<div class="insight-title">Organic</div>
				<div class="insight-body">
					The dominant descriptor. Followed by Natural (60%) and Friendly (56%). Users felt Loam was
					grounded and minimal before a single screen was designed.
				</div>
			</div>
			<div class="insight-card" data-num="62%">
				<div class="insight-title">Growth</div>
				<div class="insight-body">
					The primary emotion Loam evoked. Warmth followed at 56%, Calm at 52%. The identity of Loam
					is centered on organic qualities that inspire growth and warmth.
				</div>
			</div>
			<div class="insight-card" data-num="48%">
				<div class="insight-title">Cozy & Personal</div>
				<div class="insight-body">
					How users said Loam should feel, with Calm and Nurturing close behind at 44%. Comfort and
					serenity drove the emotional direction of the UI.
				</div>
			</div>
		</div>
		<!-- 
		<p class="body-text">
			The desirability data pointed clearly toward organic, plant-like imagery for visual
			representations of connection. Plants or roots ranked highest, followed by circles and links,
			then paths and bridges.
		</p> -->

		<p class="body-text" style="margin-top: 16px;">
			This informed both the logotype and the logomark. The final logotype uses hand-drawn letters
			characters to bring in a human touch, softened and bloated anchor points to create natural
			uneven curves, and an earthy color palette grounded in soil and nature. The logomark
			integrates leaf forms, root-like curves, and a non-perfect circular shape: a subtle abstract
			reference to L-O-A-M hidden across the top, grounded by the roots below.
		</p>

		<div class="">
			<div class="case-img-wrap">
				<video
					src="/loam-logotype.mov"
					class="case-img"
					muted
					playsinline
					autoplay
					on:ended={(e) => e.target.pause()}
				></video>
				<span class="case-img-caption">Logotype explorations & final</span>
			</div>
			<div class="case-img-wrap">
				<video
					src="/loam-logomark.mov"
					class="case-img"
					muted
					playsinline
					autoplay
					on:ended={(e) => e.target.pause()}
				></video>
				<span class="case-img-caption">Logomark explorations & final</span>
			</div>
		</div>
	</section>

	<!-- 04 PHYSICAL PRODUCT -->
	<section class="cs-section" id="physical">
		<div class="section-eyebrow">
			<span class="eyebrow-num">04</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Physical Product</span>
		</div>
		<h2>Connection doesn't<br />have to be digital.</h2>
		<p class="body-text">
			As part of Loam's identity, we wanted to bring in a physical component, an object that
			represents real-world interaction, not just digital connection. Something people could carry,
			use, and display that quietly signals: <em>"I'm a Loam user. You can connect with me."</em>
		</p>
		<p class="body-text" style="margin-top: 16px;">
			We defined four criteria: affordable, functional, user-friendly, and portable. All while
			supporting NFC tap-to-connect functionality. We explored keychains and collectible figures,
			but most only served one purpose. That's when the carabiner made the most sense.
		</p>

		<blockquote class="pull-quote">
			Simple, useful, cheap to produce — people already clip it on bags and belt loops, making it
			perfect for visibility and NFC functionality.
		</blockquote>

		<p class="body-text">
			Our team studied how carabiners work mechanically and challenged ourselves to design one that
			is fully 3D-printed with no extra hardware. After testing several functional models, we moved
			into form exploration inspired by leaves, soil, and our lettermark. Landing on a bag of soil
			and a leaf shape as the first prototype forms.
		</p>

		<div class="case-img-wrap">
			<img src="/loam-physical-1.png" alt="" class="case-img" />
			<span class="case-img-caption">Loam Carabiner sketches</span>
		</div>
	</section>

	<!-- 05 PROTOTYPING -->
	<section class="cs-section" id="prototyping">
		<div class="section-eyebrow">
			<span class="eyebrow-num">05</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Prototyping & Testing</span>
		</div>
		<h2>Two rounds of testing.<br />Real frustration, real fixes.</h2>
		<p class="body-text">
			Once we had confidently established our brand identity and voice, we moved to the design phase
			of our project. We ran prototype testing at both low and mid fidelity, using each round to
			surface assumptions we hadn't caught in design.
		</p>

		<div class="solution-list" style="margin-top: 28px;">
			<div>
				<div class="solution-item">
					<div class="solution-num">Lo-Fi</div>
					<div>
						<div class="solution-title">Clarity of purpose</div>
						<div class="solution-body">
							Multiple users stated they were "not completely clear on what the purpose of the app
							is" even after starting onboarding. Profile item category selection was also confusing
							— their mental model was discovery ("find a new album") not profile building ("add my
							own interests"). We identified critical areas of friction in content and terminology.
						</div>
					</div>
				</div>
				<div class="case-img-wrap">
					<img src="/loam-lowfi-screens.png" alt="" class="case-img" />
					<span class="case-img-caption">Low Fidelity Screens</span>
				</div>
			</div>
			<div>
				<div class="solution-item">
					<div class="solution-num">Mid-Fi</div>
					<div>
						<div class="solution-title">Logic gaps & interaction clarity</div>
						<div class="solution-body">
							Testing revealed a hole in our comment logic, requiring us to reconsider anonymous
							comment permissions. The emoji reaction process wasn't intuitive enough. Onboarding
							needed stronger branding. And posting text vs. posting media needed to be streamlined.
						</div>
					</div>
				</div>
				<div class="case-img-wrap">
					<img src="/loam-midfi-screens.png" alt="" class="case-img" />
					<span class="case-img-caption">Mid Fidelity Screens</span>
				</div>
			</div>
		</div>
	</section>

	<!-- 06 THE PRODUCT -->
	<section class="cs-section" id="product">
		<div class="section-eyebrow">
			<span class="eyebrow-num">06</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">The Product</span>
		</div>
		<h2>Every feature is a<br />deliberate choice.</h2>
		<p class="body-text">
			Loam's feature set is defined as much by what we left out as by what we built. Each decision
			was stress-tested against our core commitment: betterment of the user, not their data.
		</p>

		<div class="solution-list" style="margin-top: 32px;">
			<div class="solution-item">
				<div class="solution-num">①</div>
				<div>
					<div class="solution-title">Interest-based profiles</div>
					<div class="solution-body">
						Whether it's that song you've had on repeat or a thought you had in the shower, your
						profile reflects you — right now. Most platforms trap users in permanent archives,
						creating pressure that kills authenticity. Loam profiles are designed to be updated
						constantly, without the weight of your digital history holding you back. Users can share
						text, images, and media from books, shows, movies, songs, albums, and podcasts.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">②</div>
				<div>
					<div class="solution-title">Connection limit: 150</div>
					<div class="solution-body">
						We capped connections at 150 — rooted in Dunbar's Number, the proposed cognitive limit
						for stable, meaningful social relationships. Loam isn't for building an audience or
						chasing virality. It's strictly for staying connected with you and yours.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">③</div>
				<div>
					<div class="solution-title">Metric free</div>
					<div class="solution-body">
						Like, follower, and comment counts aren't publicly displayed. Traditional platforms
						condition us to judge value by metrics. We believe value should be tied to the meaning
						and quality of connection — not oversimplifying statistics. A completely metric-free
						environment designed for genuine interaction, not data collection.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">④</div>
				<div>
					<div class="solution-title">Chronological feed</div>
					<div class="solution-body">
						Your feed shows the most recent posts first. No algorithms, no manipulation — just the
						people you're connected with, in the order they shared. We don't want your attention. We
						want your people to have it.
					</div>
				</div>
			</div>
			<div class="solution-item">
				<div class="solution-num">⑤</div>
				<div>
					<div class="solution-title">Branches</div>
					<div class="solution-body">
						A layer beyond connections. When you make a branch, you add specific connections to it.
						You can post to specific branches and organize your feed by them — giving you another
						opportunity to share in an authentic, intentional way.
					</div>
				</div>
			</div>
		</div>

		<div class="case-img-wrap">
			<img
				src="/loam-final-screens.png"
				alt="Screenshot of the final product screens"
				class="case-img"
			/>
			<span class="case-img-caption">Final Product Screens</span>
		</div>
	</section>

	<!-- 07 MVP & OUTCOMES -->
	<section class="cs-section" id="outcomes">
		<div class="section-eyebrow">
			<span class="eyebrow-num">07</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">MVP & Outcomes</span>
		</div>
		<h2>50 users and counting. Real behavior.<br />The proof is in the pudding.</h2>
		<p class="body-text">
			After building a confident prototype we shipped a live MVP web-app. After having a confident
			prototype we moved on to build a live MVP web-app for loam. We built the app using Svelte,
			SCSS, and nodeJS. We used Supabase for our database, Cloudinary for image transformation and
			storage, and Resend for communication with users.
		</p>
		<br />
		<p class="bod-text">
			40 users used it regularly — including us. This was an opportunity to surface behavioral
			patterns that prototype testing simply can't unearth.
		</p>

		<div class="case-img-wrap">
			<img
				src="/loam-mvp-survey.png"
				alt="Screenshot of the original leaderboard design, showing a ranked list of students with their points and levels"
				class="case-img"
			/>
			<span class="case-img-caption">MVP exit survey results</span>
		</div>

		<!-- <div class="kpi-band">
			<div class="kpi-item">
				<div class="kpi-num">63%</div>
				<div class="kpi-label">
					Say they have a healthier relationship<br />with social media after using Loam
				</div>
			</div>
			<div class="kpi-divider"></div>
			<div class="kpi-item">
				<div class="kpi-num">100%</div>
				<div class="kpi-label">
					Say Loam improves their relationships<br />by keeping them connected
				</div>
			</div>
			<div class="kpi-divider"></div>
			<div class="kpi-item">
				<div class="kpi-num">8/10</div>
				<div class="kpi-label">Average satisfaction score<br />with Loam</div>
			</div>
		</div> -->

		<p class="body-text">
			Compare that to the 6/10 average satisfaction with existing social platforms we found in our
			initial research. In 10 months, starting from a pitch and a shared belief, we built something
			that genuinely moved people's relationship with social media.
		</p>
		<p class="body-text" style="margin-top: 16px;">
			This isn't a case study about revenue or engagement. It's about building something that
			matters — and proving, with real users, that it does.
		</p>
	</section>

	<!-- 06.5 INTENTIONAL FRICTION -->
	<section class="cs-section" id="friction">
		<div class="section-eyebrow">
			<span class="eyebrow-num">08</span>
			<span class="eyebrow-line"></span>
			<span class="eyebrow-label">Intentional Friction</span>
		</div>
		<h2>Building with<br />discipline.</h2>
		<p class="body-text">
			Intention is a core aspect of Loam's ethos, we want our users to be intentional about how, and
			to who, they give their time online. Nowhere is this more deliberate than in how connections
			are made.
		</p>
		<p class="body-text">
			There is no way to search for users or receive suggestions for connections in the app. When a
			user signs up for loam, we want them to give thought to who they'd like to be connected with
			and go out of their way to invite those individuals to connect. Our hope was to make it a
			process that was mindful, not frictionless.
		</p>

		<blockquote class="pull-quote">
			"We want every connection on Loam to be a reflection of a real connection in your life."
		</blockquote>

		<p class="body-text">
			We noticed something unexpected during the MVP: users were signing up and not connecting with
			anyone. There was a preexisting expectation that Loam would do the heavy lifting — that there
			would be suggestions, a discovery page, an easy way to find people they might know. Some users
			wanted to search by name. Some wanted a public list of everyone on the app.
		</p>
		<p class="body-text">
			This was a tempting, and objectively effective, fix. We had around 50 users, most invited by
			our team, most friends with each other. Most not connected. A basic suggestion algorithm or a
			full user list would've created many immediate connections. It could've been the kickstart the
			app needed.
		</p>

		<div class="friction-moment">
			<div class="friction-side">
				<div class="friction-label">The easy path</div>
				<div class="friction-body">
					Ship a suggestion algorithm. Show a user list. Watch connections spike. Ship it, call it
					done.
				</div>
			</div>
			<div class="friction-divider">→</div>
			<div class="friction-side friction-side--chosen">
				<div class="friction-label">What we chose</div>
				<div class="friction-body">
					Hold off. Wait. See if and how it could happen organically. Trust the design.
				</div>
			</div>
		</div>

		<p class="body-text">
			Over time, we noticed users started finding each other on Loam. Where? In person. Users who
			spent meaningful time together eventually talked about Loam, realized they were both on it,
			and connected in that moment. A connection that wasn't handed to them but discovered through
			real-world interaction.
		</p>
		<p class="body-text">
			By maintaing a certain friction to the process, every connection on Loam became a reflection
			of a genuine relationship. Users were building their own social environments instead of
			standing by while an algorithm did it for them.
		</p>

		<blockquote class="pull-quote">
			"Think about how you'd perceive a sweater you hand-knit yourself versus one you got for free
			at a company event. Where there is effort, there is pride."
		</blockquote>

		<p class="body-text">
			Allowing friction to exist where it should and avoiding the quick fix is what makes Loam as
			special as it is. This was one of the hardest decisions we made as a team, and the one I'm
			most proud of.
		</p>
		<a href="https://loam.ing" target="_blank" rel="noopener noreferrer" class="live-link">
			Visit Loam — loam.ing ↗
		</a>
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
		font-size: clamp(120px, 22vw, 260px);
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
		font-size: clamp(52px, 9vw, 90px);
		font-weight: 400;
		line-height: 1.05;
		letter-spacing: -3px;
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

	/* ─── TEAM GRID ─── */
	.team-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 12px;
		margin: 28px 0;
	}

	.team-item {
		padding: 16px 18px;
		border: 1.5px solid var(--light-stone);
		border-radius: 6px;
		background: var(--cream);
	}

	.team-item--me {
		border-color: var(--clay);
		background: var(--sand);
	}

	.team-name {
		font-size: 15px;
		font-weight: 500;
		color: var(--ink);
		margin-bottom: 4px;
	}

	.team-role {
		font-family: 'Caveat', cursive;
		font-size: 14px;
		color: var(--stone);
	}

	.team-item--me .team-role {
		color: var(--bark);
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
		font-size: 16px;
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
		grid-template-columns: 56px 1fr;
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
		margin-bottom: 8px;
	}
	.solution-body {
		font-size: 15px;
		line-height: 1.75;
		color: #4a4440;
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
		margin: 12px 0;
	}

	.img-grid-3 {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		gap: 14px;
		margin: 36px 0;
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
	}
	.kpi-divider {
		width: 1px;
		background: rgba(255, 255, 255, 0.1);
		align-self: stretch;
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
		.team-grid {
			grid-template-columns: 1fr 1fr;
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

	/* ─── FRICTION MOMENT ─── */
	.friction-moment {
		display: grid;
		grid-template-columns: 1fr 32px 1fr;
		align-items: center;
		gap: 0;
		margin: 36px 0;
		background: var(--cream);
		border: 1.5px solid var(--light-stone);
		border-radius: 8px;
		overflow: hidden;
	}

	.friction-side {
		padding: 24px 28px;
	}

	.friction-side--chosen {
		background: var(--sand);
		border-left: 3px solid var(--clay);
	}

	.friction-label {
		font-family: 'Caveat', cursive;
		font-size: 13px;
		color: var(--stone);
		letter-spacing: 1.5px;
		text-transform: uppercase;
		margin-bottom: 10px;
	}

	.friction-side--chosen .friction-label {
		color: var(--clay);
	}

	.friction-body {
		font-size: 15px;
		line-height: 1.75;
		color: #4a4440;
	}

	.friction-divider {
		text-align: center;
		font-family: 'Caveat', cursive;
		font-size: 22px;
		color: var(--stone);
		opacity: 0.5;
	}

	@media (max-width: 700px) {
		.friction-moment {
			grid-template-columns: 1fr;
		}
		.friction-divider {
			transform: rotate(90deg);
			padding: 8px 0;
		}
		.friction-side--chosen {
			border-left: none;
			border-top: 3px solid var(--clay);
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

	.live-link {
		display: inline-block;
		margin-top: 40px;
		font-family: 'Caveat', cursive;
		font-size: 20px;
		color: var(--clay);
		text-decoration: none;
		border-bottom: 1.5px solid var(--clay);
		padding-bottom: 2px;
		transition:
			color 0.2s,
			border-color 0.2s;
	}

	.live-link:hover {
		color: var(--bark);
		border-color: var(--bark);
	}
</style>
