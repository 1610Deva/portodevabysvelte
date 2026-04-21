<script lang="ts">
	import { onMount } from 'svelte';

	interface Technology {
		name: string;
		icon: string;
		color: string;
	}

	interface TechnologiesData {
		frontend: Technology[];
		backend: Technology[];
		uidesign: Technology[];
		tools: Technology[];
	}

	interface Experience {
		type: string;
		position: string;
		period: string;
		company: string;
		description: string;
		workingtype: string;
		color: string;
	}

	interface Education {
		degree: string;
		period: string;
		institution: string;
		description: string;
		gpa?: string;
		color: string;
	}

	interface Organization {
		id: number;
		position: string;
		'organization-name': string;
		period: string;
		description: string;
		color: string;
	}

	interface Achievement {
		icon: string;
		title: string;
		date: string;
		organization: string;
		description: string;
		color: string;
	}

	let isVisible = false;

	let technologies: TechnologiesData = {
		frontend: [],
		backend: [],
		uidesign: [],
		tools: []
	};
	let experiences: Experience[] = [];
	let education: Education[] = [];
	let organizations: Organization[] = [];
	let achievements: Achievement[] = [];

	let activeTab: 'work' | 'education' | 'achievements' | 'organization' = 'work';

	// Reactive statement Svelte
	$: filteredExperiences = experiences.filter((exp) => exp.type === 'work');

	onMount(async () => {
		setTimeout(() => {
			isVisible = true;
		}, 300);
		try {
			const res = await fetch('/data/data.json');
			if (!res.ok) throw new Error('Gagal mengambil data');

			const data = await res.json();
			technologies = data.technologies || technologies;
			experiences = data.experiences || [];
			education = data.education || [];
			organizations = data.organization || [];
			achievements = data.achievements || [];
		} catch (error) {
			console.error('Error fetching data:', error);
		}
	});

	function getColorClasses(color: string) {
		const colorMap: Record<string, { bg: string; border: string; text: string }> = {
			cyan: { bg: 'bg-cyan-500/10', border: 'border-cyan-500/30', text: 'text-cyan-400' },
			pink: { bg: 'bg-pink-500/10', border: 'border-pink-500/30', text: 'text-pink-400' },
			blue: { bg: 'bg-blue-500/10', border: 'border-blue-500/30', text: 'text-blue-400' },
			yellow: { bg: 'bg-yellow-500/10', border: 'border-yellow-500/30', text: 'text-yellow-400' },
			purple: { bg: 'bg-purple-500/10', border: 'border-purple-500/30', text: 'text-purple-400' },
			green: { bg: 'bg-green-500/10', border: 'border-green-500/30', text: 'text-green-400' },
			red: { bg: 'bg-red-500/10', border: 'border-red-500/30', text: 'text-red-400' }
		};
		return colorMap[color] || colorMap.cyan;
	}
</script>

<svelte:head>
	<title>About - Devadatta Giri</title>
</svelte:head>

<!-- HEADER SECTION -->
<!-- <div
	class="md:mx-5 mt-3 rounded-xl p-10 transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<div class="text-center">
		<h1 class="mb-4 text-4xl font-bold text-white">
			About Me
		</h1>
		<p class="mx-auto max-w-2xl text-lg text-gray-300">
			Get to know more about who I am, my background, skills, and what drives my passion for
			technology and design.
		</p>
	</div>
</div> -->

<!-- INTRODUCTION SECTION -->
<div
	class="order-2 md:order-1 md:mx-5 mt-3 grid grid-cols-1 gap-6 rounded-xl border border-white/10 bg-slate-900/80 p-10 shadow-lg transition-opacity duration-1000 ease-in-out md:grid-cols-2"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<!-- Profile Image -->
	<div class="flex items-center justify-center order-1 md:order-2">
		<div class="overflow-hidden rounded-lg border-4 border-blue-400/30 shadow-xl">
			<img
				src="../assets/img/deva2.jpeg"
				alt="Devadatta Giri"
				class="h-auto w-full max-w-md object-cover transition-transform duration-300 hover:scale-105"
				loading="lazy"
			/>
		</div>
	</div>

	<!-- About Text -->
	<div class="flex flex-col justify-center p-4 order-2 md:order-1">
		<!-- <h5 class="inline-block mb-5 text-base font-semibold text-white md:text-lg">
			<span class="text-amber-100 bg-blue-900 px-10 py-2">ABOUT ME</span>
		</h5> -->
		<h2 class="mb-7 text-md md:text-3xl font-bold text-white">
			<span class="px-15 py-3 bg-blue-900 rounded-lg">🧑‍💻 Get To Know Me!</span>
		</h2>
		<p class="mb-4 text-lg leading-relaxed text-gray-300 text-justify">
			Hi! I'm <span class="font-semibold text-white">I Made Nandana Devadatta Giri</span>, a
			passionate <span class="border-b-4 border-blue-500">Frontend Developer</span> and <span class="border-b-4 border-blue-500">UI/UX Designer</span> based in Surabaya,
			Indonesia. I specialize in creating beautiful, functional, and user-friendly web experiences.
		</p>
		<p class="mb-4 text-lg leading-relaxed text-gray-300 text-justify">
			I am interested in programming and design, especially website development, application design,
			and digital marketing. I have been interested in these fields for more than three years and
			continuously learning new technologies to improve my skills.
		</p>
		<p class="mb-6 text-lg leading-relaxed text-gray-300 text-justify">
			Currently, I'm pursuing my Bachelor's degree in Informatics Engineering at State University of
			Surabaya with a GPA of 3.89/4.00, where I'm also serving as a Software Development Laboratory
			Assistant.
		</p>
	</div>
</div>

<!-- WHAT I DO SECTION -->
<div
	class="md:mx-5 mt-3 rounded-xl border border-white/10 bg-slate-900/80 p-10 shadow-lg transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<h2 class="mb-8 text-xl md:text-3xl font-bold text-white">
		<span class="px-15 py-3 bg-blue-900 shadow-lg rounded-lg ">📝 What I'm Doing</span>
	</h2>

	<div class="grid grid-cols-1 gap-6 md:grid-cols-3">
		<!-- Frontend Development -->
		<div
			class="rounded-lg border border-blue-400/30 bg-blue-500/5 p-6 transition-all hover:border-blue-400/50 hover:bg-blue-500/10"
		>
			<div class="mb-4 text-center">
				<i class="fa-solid fa-code text-5xl text-blue-400"></i>
			</div>
			<h3 class="mb-3 text-center text-xl font-semibold text-white">Frontend Development</h3>
			<p class="text-center text-gray-300">
				Building responsive and interactive web applications using modern frameworks like React &
				Svelte with focus on performance and user experience.
			</p>
		</div>

		<!-- UI/UX Design -->
		<div
			class="rounded-lg border border-pink-400/30 bg-pink-500/5 p-6 transition-all hover:border-pink-400/50 hover:bg-pink-500/10"
		>
			<div class="mb-4 text-center">
				<i class="fa-solid fa-pen-nib text-5xl text-pink-400"></i>
			</div>
			<h3 class="mb-3 text-center text-xl font-semibold text-white">UI/UX Design</h3>
			<p class="text-center text-gray-300">
				Designing intuitive and aesthetically pleasing user interfaces using Figma. Creating
				wireframes, prototypes, and design systems that enhance user satisfaction.
			</p>
		</div>

		<!-- Web Design -->
		<div
			class="rounded-lg border border-purple-400/30 bg-purple-500/5 p-6 transition-all hover:border-purple-400/50 hover:bg-purple-500/10"
		>
			<div class="mb-4 text-center">
				<i class="fa-solid fa-palette text-5xl text-purple-400"></i>
			</div>
			<h3 class="mb-3 text-center text-xl font-semibold text-white">Web Design</h3>
			<p class="text-center text-gray-300">
				Crafting beautiful landing pages and websites with attention to detail, modern design
				principles, and best practices in accessibility and responsiveness.
			</p>
		</div>
	</div>
</div>

<!-- TIMELINE SECTION -->
<div
	class="md:mx-5 mt-3 rounded-xl border border-white/10 bg-slate-900/80 p-10 shadow-lg transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<h2 class="mb-8 text-xl md:text-3xl font-bold text-white">
		<span class="px-15 py-3 bg-blue-900 rounded-lg">🏄‍♂️ My Journey</span>
	</h2>

	<!-- Tab Navigation -->
	<div class="mb-8 flex md:overflow-hidden overflow-scroll gap-4">
		<button
			class="text-sm md:text-md rounded-lg px-6 py-3 font-semibold transition-all"
			class:bg-blue-600={activeTab === 'work'}
			class:text-white={activeTab === 'work'}
			class:bg-white={activeTab !== 'work'}
			class:text-blue-900={activeTab !== 'work'}
			class:hover:bg-white={activeTab !== 'work'}
			on:click={() => (activeTab = 'work')}
		>
			<i class="fa-solid fa-briefcase mr-2"></i>
			Work Experience
		</button>
		<button
			class="text-sm md:text-md rounded-lg px-6 py-3 font-semibold transition-all"
			class:bg-blue-600={activeTab === 'education'}
			class:text-white={activeTab === 'education'}
			class:bg-white={activeTab !== 'education'}
			class:text-blue-900={activeTab !== 'education'}
			class:hover:bg-white={activeTab !== 'education'}
			on:click={() => (activeTab = 'education')}
		>
			<i class="fa-solid fa-graduation-cap mr-2"></i>
			Education
		</button>
		<button
			class="text-sm md:text-md rounded-lg px-6 py-3 font-semibold transition-all"
			class:bg-blue-600={activeTab === 'organization'}
			class:text-white={activeTab === 'organization'}
			class:bg-white={activeTab !== 'organization'}
			class:text-blue-900={activeTab !== 'organization'}
			class:hover:bg-white={activeTab !== 'organization'}
			on:click={() => (activeTab = 'organization')}
		>
			<i class="fa-solid fa-user-group mr-2"></i>
			Organization
		</button>
		<button
			class="text-sm md:text-md rounded-lg px-6 py-3 font-semibold transition-all"
			class:bg-blue-600={activeTab === 'achievements'}
			class:text-white={activeTab === 'achievements'}
			class:bg-white={activeTab !== 'achievements'}
			class:text-blue-900={activeTab !== 'achievements'}
			class:hover:bg-white={activeTab !== 'achievements'}
			on:click={() => (activeTab = 'achievements')}
		>
			<i class="fa-solid fa-trophy mr-2"></i>
			Achievements
		</button>
	</div>

	<!-- Work Experience Tab -->
	{#if activeTab === 'work'}
		<div class="space-y-4">
			{#each filteredExperiences as exp}
				{@const colors = getColorClasses(exp.color)}
				<div
					class="rounded-lg border p-6 transition-all hover:scale-[1.02] {colors.bg} {colors.border}"
				>
					<div class="mb-3 flex flex-col items-start justify-between md:flex-row md:items-center">
						<h3 class="text-xl font-semibold text-white">{exp.position}</h3>
						<span
							class="mt-2 rounded-full px-3 py-1 text-sm font-medium md:mt-0 {colors.bg} {colors.text}"
						>
							{exp.period}
						</span>
					</div>
					<p class="mb-2 font-medium {colors.text}">
						<i class="fa-solid fa-building mr-2"></i>
						{exp.company}
					</p>
					<p class="mb-3 text-gray-300">{exp.description}</p>
					<div class="flex gap-2">
						<span class="rounded-full bg-white/10 px-3 py-1 text-xs text-white">
							<i class="fa-solid fa-briefcase mr-1"></i>
							{exp.workingtype}
						</span>
					</div>
				</div>
			{/each}
		</div>
	{/if}

	<!-- Education Tab -->
	{#if activeTab === 'education'}
		<div class="space-y-4">
			{#each education as edu}
				{@const colors = getColorClasses(edu.color)}
				<div
					class="rounded-lg border p-6 transition-all hover:scale-[1.02] {colors.bg} {colors.border}"
				>
					<div class="mb-3 flex flex-col items-start justify-between md:flex-row md:items-center">
						<h3 class="text-xl font-semibold text-white">{edu.degree}</h3>
						<span
							class="mt-2 rounded-full px-3 py-1 text-sm font-medium md:mt-0 {colors.bg} {colors.text}"
						>
							{edu.period}
						</span>
					</div>
					<p class="mb-2 font-medium {colors.text}">
						<i class="fa-solid fa-school mr-2"></i>
						{edu.institution}
					</p>
					<p class="mb-3 text-gray-300">{edu.description}</p>
					{#if edu.gpa}
						<div class="flex gap-2">
							<span class="rounded-full bg-white/10 px-3 py-1 text-xs text-white">
								<i class="fa-solid fa-star mr-1"></i>
								GPA: {edu.gpa}
							</span>
						</div>
					{/if}
				</div>
			{/each}
		</div>
	{/if}

	<!-- Organization Tab -->
	{#if activeTab === 'organization'}
		<div class="space-y-4">
			{#each organizations as org}
				{@const colors = getColorClasses(org.color)}
				<div
					class="rounded-lg border p-6 transition-all hover:scale-[1.02] {colors.bg} {colors.border}"
				>
					<div class="mb-3 flex flex-col items-start justify-between md:flex-row md:items-center">
						<h3 class="text-xl font-semibold text-white">{org.position}</h3>
						<span
							class="mt-2 rounded-full px-3 py-1 text-sm font-medium md:mt-0 {colors.bg} {colors.text}"
						>
							{org.period}
						</span>
					</div>
					<p class="mb-2 font-medium {colors.text}">
						<i class="fa-solid fa-school mr-2"></i>
						{org['organization-name']}
					</p>
					<p class="mb-3 text-gray-300">{org.description}</p>
					{#if org['organization-name']}
						<div class="flex gap-2">
							<span class="rounded-full bg-white/10 px-3 py-1 text-xs text-white">
								<i class="fa-solid fa-school mr-1"></i>
								{org['organization-name']}
							</span>
						</div>
					{/if}
				</div>
			{/each}
		</div>
	{/if}

	<!-- Achievements Tab -->
	{#if activeTab === 'achievements'}
		<div class="space-y-4">
			{#each achievements as achievement}
				{@const colors = getColorClasses(achievement.color)}
				<div
					class="rounded-lg border p-6 transition-all hover:scale-[1.02] {colors.bg} {colors.border}"
				>
					<div class="mb-3 flex items-start gap-4">
						<div class="rounded-full p-3 {colors.bg}">
							<i class="fa-solid {achievement.icon} text-2xl {colors.text}"></i>
						</div>
						<div class="flex-1">
							<div
								class="mb-2 flex flex-col items-start justify-between md:flex-row md:items-center"
							>
								<h3 class="text-xl font-semibold text-white">{achievement.title}</h3>
								<span class="mt-2 text-sm md:mt-0 {colors.text}">
									{achievement.date}
								</span>
							</div>
							<p class="mb-2 font-medium {colors.text}">
								<i class="fa-solid fa-building mr-2"></i>
								{achievement.organization}
							</p>
							<p class="text-gray-300">{achievement.description}</p>
						</div>
					</div>
				</div>
			{/each}
		</div>
	{/if}
</div>

<!-- CONTACT CTA -->
<div
	class="md:mx-5 mt-3 rounded-xl border border-blue-500/20 bg-gradient-to-r from-blue-950/60 to-purple-950/60 p-10 shadow-lg transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<div class="text-center">
		<h2 class="mb-4 text-3xl font-bold text-white">Let's Work Together!</h2>
		<p class="mx-auto mb-6 max-w-2xl text-lg text-gray-300">
			I'm always open to discussing new projects, creative ideas, or opportunities to be part of
			your vision. Feel free to reach out!
		</p>
		<div class="flex flex-wrap justify-center gap-4">
			<a
				href="/assets/cv/CV-Devadatta-Giri.pdf"
				download="CV-Devadatta-Giri.pdf"
				target="_blank"
				class="rounded-lg bg-blue-600 px-6 py-3 font-semibold text-white transition hover:bg-blue-700"
			>
				<i class="fa-solid fa-download mr-2"></i>
				Download CV
			</a>
			<a
				href="/projects"
				class="rounded-lg border border-white bg-transparent px-6 py-3 font-semibold text-white transition hover:bg-white/10"
			>
				<i class="fa-solid fa-folder-open mr-2"></i>
				View My Projects
			</a>
		</div>
	</div>
</div>
