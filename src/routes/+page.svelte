<script lang="ts">
	import resume from '$lib/assets/Resume_EP.pdf';
	import Project from '$lib/Project.svelte';

	let { data } = $props();

	const images: string[] = Array.isArray(data.images?.url)
		? data.images.url
		: data.images?.url
			? [data.images.url]
			: [];

	const name: string = 'Eddie Poulson';
	const splitName: string[] = name.split('');

	function scrollIntoView({ target }: { target: EventTarget | null }) {
		const href = document.querySelector((target as HTMLElement).getAttribute('href') ?? '');
		if (!href) {
			return;
		} else {
			href.scrollIntoView({
				behavior: 'smooth'
			});
		}
	}

	function scrollToTop(event: MouseEvent) {
		event.preventDefault();
		window.scrollTo({ top: 0, behavior: 'instant' });
	}
</script>

<svelte:head>
	<title>{name}</title>
</svelte:head>
<nav class="site-nav">
	<a href="#top" class="nav-name" aria-label="Back to top" onclick={scrollToTop}>
		<div class="name-lockup" aria-hidden="true">
			{#each splitName as char}
				<span class={char === ' ' ? 'name-space' : ''}>
					{char === ' ' ? '\u00A0' : char}
				</span>
			{/each}
		</div>
		<span class="nav-role">/ software engineer</span>
	</a>
	<div class="nav-links">
		<a href="#about-me" onclick={scrollIntoView}>about</a>
		<a href="#projects" onclick={scrollIntoView}>projects</a>
		<a href={resume} download class="nav-resume">résumé</a>
	</div>
</nav>
<main>
	<section class="hero" id="top" aria-labelledby="hero-title">
		<div class="hero-copy">
			<h1 id="hero-title">
				Passionate about creating efficient software, and working on whatever's currently
				<span>in my garage.</span>
			</h1>
			<div class="hero-footer">
				<div class="social-links">
					<a href="https://github.com/eddipoulson" target="_blank" rel="noreferrer">
						GitHub
					</a>
					<a href="https://www.linkedin.com/in/eddie-poulson/" target="_blank" rel="noreferrer">
						LinkedIn
					</a>
				</div>
			</div>
		</div>
	</section>

	{#if images.length}
		<section class="carousel-shell" aria-label="Highlights from the garage">
			<div class="flex w-max gap-1" id="carousel">
				{#each images as image}
					<img src={image} alt="" class="carousel-image" />
				{/each}
				{#each images as image}
					<img src={image} alt="" class="carousel-image" />
				{/each}
			</div>
		</section>
	{/if}

	<section class="about-section" id="about-me">
		<div class="section-heading">
			<p>01 / 02</p>
			<h2>About</h2>
		</div>
		<div class="about-grid">
			<div class="about-copy">
				<p class="about-lead">
					I'm a software engineer from Southern California, as well as a bit of an
					<em>aspiring</em> race car driver.
				</p>
				<p>
					Currently working at
					<a href="https://www.linkedin.com/company/capital-group/" target="_blank" rel="noreferrer">
						Capital Group
					</a>, where I spend most of my time making my team's projects more efficient.
					<br /><br />
					Outside of all of that computer business, I'm a big car guy. I would love any
					opportunity to combine my passion for cars and software, should an opportunity
					present itself!
				</p>
			</div>
			<dl class="details">
				<div>
					<dt>Currently</dt>
					<dd>Contracted Software Engineer<br />Capital Group · Network Management</dd>
				</div>
				<div>
					<dt>Stable</dt>
					<dd>’78 Porsche 911SC Targa<br />’23 Audi A5 Sportback<br />’01 BMW 325iT LeMons car</dd>
				</div>
			</dl>
		</div>
	</section>

	<section class="projects-section" id="projects">
		<div class="section-heading">
			<p>02 / 02</p>
			<h2>Projects</h2>
		</div>
		<div class="project-grid">
		<Project
			name="carcult"
			description="
        Created by car enthusiasts, for car enthusiats. This aims to be the shortest possible path from enthusiast to meet. Probably being rewritten and redesigned again.
        "
			source="https://github.com/eddipoulson/carcult"
			link="https://carcult.org"
		/>
		<Project
			name="obelisk"
			description="
        The big thing that I work on at Capital Group! A Django monolith that integrates with LogicMonitor to track thousands of network devices and surface alerts to the NOC. I've focused on improving performance and reliability by introducing caching strategies, cutting down N+1 queries, and refactoring core modules. I also built onboarding workflows that let admins quickly bring in devices from both cloud and physical sources, streamlining how our teams manage critical infrastructure.
        "
		/>
		<Project
			name="DigiDigits"
			description="
        Utilizes the TCGPlayer API to store market price data for Digimon cards in a SQLite database to create datasets. 
        Future plans include using time-series forecasting and regression anaylsis to find optimal times to buy and sell cards."
			source="https://github.com/eddipoulson/DigiDigits"
		/>
		<Project
			name="shortstack"
			description="A solution to a problem I had with sending FB Marketplace links to friends of mine. Had a fun little pancake theme to it and a feed feature to see what links people were 'stacking'!"
			source="https://github.com/eddipoulson/shortstack"
		/>
		<Project
			name="Animal Log"
			description="PWA for tracking exotic pet feeding schedules, QR-tagged tanks, mobile-first, and built to solve my fiancée's problem of remembering what animals were fed when."
			source="https://github.com/eddipoulson/animal-log"
			link="https://animal-log.vercel.app/"
		/>
		<Project
			name="Jotsync"
			description="A glorified notepad web app. It utilizes PocketBase's realtime functionality to allow users to create notes and then share and collaborate on them in realtime. Has a link sharing system and that's really all there is to it."
			source="https://github.com/eddipoulson/jotsync"
			link="https://jotsync.vercel.app"
		/>
		</div>
	</section>
</main>
<footer>
	<p>Eddie Poulson</p>
	<a href="#top" aria-label="Back to top" onclick={scrollToTop}>Top ↑</a>
</footer>
