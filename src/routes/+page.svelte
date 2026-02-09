<script lang="ts">
	import { onDestroy, onMount } from 'svelte';

	let isVisible = false;

	// Speciality Animation
	const specialities = ['Junior Frontend Developer 🌐', 'UI/UX Designer ✒️', 'Web Designer 🧩'];

	let specialityIndex = 0;
	let displayedSpeciality = '';
	let typingTimeout: ReturnType<typeof setTimeout> | undefined;

	function typeSpeciality(text: string, i = 0) {
		if (i <= text.length) {
			displayedSpeciality = text.slice(0, i);
			typingTimeout = setTimeout(() => typeSpeciality(text, i + 1), 65);
		} else {
			typingTimeout = setTimeout(() => deleteSpeciality(text), 1200);
		}
	}

	function deleteSpeciality(text: string, i = text.length) {
		if (i >= 0) {
			displayedSpeciality = text.slice(0, i);
			typingTimeout = setTimeout(() => deleteSpeciality(text, i - 1), 40);
		} else {
			specialityIndex = (specialityIndex + 1) % specialities.length;
			typeSpeciality(specialities[specialityIndex]);
		}
	}

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

	interface Project {
		title: string;
		description: string;
		link: string;
		image: string;
		tags: string[];
		featured?: boolean;
	}

	interface Experience {
		id: number;
		company: string;
		position: string;
		period: string;
		description: string;
		type: string;
		workingtype: string;
		color: string;
	}

	interface Education {
		id: number;
		institution: string;
		degree: string;
		period: string;
		description: string;
		gpa?: string;
		color: string;
	}

	interface Achievement {
		id: number;
		title: string;
		organization: string;
		date: string;
		description: string;
		icon: string;
		color: string;
	}

	let technologies: TechnologiesData = {
		frontend: [],
		backend: [],
		uidesign: [],
		tools: []
	};
	let projects: Project[] = [];
	let experiences: Experience[] = [];
	let education: Education[] = [];
	let achievements: Achievement[] = [];

	// section Timeline Tab state
	let activeTab: 'work' | 'education' | 'achievements' = 'work';

	$: selectedProjects = projects.filter((p) => p.featured);
	$: filteredExperiences = experiences.filter((exp) => exp.type === 'work');

	onMount(async () => {
		isVisible = true;
		typeSpeciality(specialities[specialityIndex]);

		const res = await fetch('/data/data.json');
		const data = await res.json();
		technologies = data.technologies;
		projects = data.projects;
		experiences = data.experiences || [];
		education = data.education || [];
		achievements = data.achievements || [];
	});

	onDestroy(() => {
		if (typingTimeout) clearTimeout(typingTimeout);
	});

	function getColorClasses(color: string) {
		const colorMap: Record<string, { bg: string; border: string; text: string }> = {
			cyan: { bg: 'bg-cyan-500/10', border: 'border-cyan-500/30', text: 'text-cyan-400' },
			pink: { bg: 'bg-pink-500/10', border: 'border-pink-500/30', text: 'text-pink-400' },
			blue: { bg: 'bg-blue-500/10', border: 'border-blue-500/30', text: 'text-blue-400' },
			yellow: { bg: 'bg-yellow-500/10', border: 'border-yellow-500/30', text: 'text-yellow-400' },
			purple: { bg: 'bg-purple-500/10', border: 'border-purple-500/30', text: 'text-purple-400' }
		};
		return colorMap[color] || colorMap.cyan;
	}
</script>

<svelte:head>
	<title>PortoDevadatta by Devadatta Giri</title>
</svelte:head>

<div
	class="mt-3 grid grid-cols-1 rounded-md bg-white/5 p-10 shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out md:grid-cols-2"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<!-- Left Side -->
	<div class="my-auto p-4">
		<h1 class="mb-3 text-4xl font-bold text-white">Hi, I'm Devadatta Giri👋</h1>
		<h3 class="text-md my-5 font-semibold text-blue-800 md:text-2xl">
			<span class="rounded-xs bg-white px-4 py-2 md:px-8"
				>I'm a {displayedSpeciality} <span class="animate-pulse">|</span></span
			>
		</h3>
		<h5 class="text-md mb-4"><i class="fa-solid fa-location-dot mr-2"></i> Surabaya, Indonesia</h5>
		<p class="my-7 text-lg text-gray-300">
			I am interested in programming and design, especially website development, application design,
			and digital marketing. I have been interested in these fields for more than three years.
		</p>
		<div class="flex">
			<a
				href="/assets/cv/CV-Devadatta-Giri.pdf"
				download="CV-Devadatta-Giri.pdf"
				aria-label="Download CV"
				target="_blank"
				class="mr-4 rounded bg-sky-900 px-4 py-2 text-white transition hover:bg-blue-800"
				><i class="fa-solid fa-download mr-3" style="color: #ffffff;"></i>Download CV</a
			>
			<a
				href="#projects"
				class="rounded border border-white px-4 py-2 text-white transition hover:border-blue-800 hover:bg-blue-800"
				>My Projects</a
			>
		</div>
	</div>

	<!-- Right Side -->
	<div class="ml-3 p-4">
		<img src="../assets/img/test1.jpg" class="rounded-full" alt="Devadatta Giri" loading="lazy" />
	</div>
</div>

<!-- TECH STACK -->
<div
	class="mt-3 rounded-md bg-white/5 p-10 shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<h2 class="mb-8 text-3xl font-bold text-white">🧩 Tech Stack</h2>

	<!-- Grid Layout untuk Cards -->
	<div class="grid grid-cols-1 gap-6 md:grid-cols-2">
		<!-- Frontend Card -->
		<div
			class="rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-blue-400/50"
		>
			<h3 class="mb-4 flex items-center gap-2 text-xl font-semibold text-blue-400">
				<i class="fa-solid fa-code"></i>
				Frontend
			</h3>
			<div class="flex flex-wrap gap-2">
				{#each technologies.frontend as tech}
					<div
						class="flex items-center gap-2 rounded-full bg-white/10 px-3 py-1.5 text-sm shadow transition hover:bg-white/20"
						style="color: {tech.color}"
					>
						{#if tech.icon.startsWith('http') || tech.icon.startsWith('..')}
							<img src={tech.icon.replace('..', '')} alt={tech.name} class="h-4 w-4" />
						{:else if tech.icon.startsWith('<svg')}
							<span class="inline-flex h-4 w-4 items-center">
								{@html tech.icon}
							</span>
						{:else}
							<span class="text-base">{tech.icon}</span>
						{/if}
						<span class="font-medium text-white">{tech.name}</span>
					</div>
				{/each}
			</div>
		</div>

		<!-- Backend Card -->
		<div
			class="rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-red-400/50"
		>
			<h3 class="mb-4 flex items-center gap-2 text-xl font-semibold text-red-400">
				<i class="fa-solid fa-server"></i>
				Backend
			</h3>
			<div class="flex flex-wrap gap-2">
				{#each technologies.backend as tech}
					<div
						class="flex items-center gap-2 rounded-full bg-white/10 px-3 py-1.5 text-sm shadow transition hover:bg-white/20"
						style="color: {tech.color}"
					>
						{#if tech.icon.startsWith('http') || tech.icon.startsWith('..')}
							<img src={tech.icon.replace('..', '')} alt={tech.name} class="h-4 w-4" />
						{:else if tech.icon.startsWith('<svg')}
							<span class="inline-flex h-4 w-4 items-center">
								{@html tech.icon}
							</span>
						{:else}
							<span class="text-base">{tech.icon}</span>
						{/if}
						<span class="font-medium text-white">{tech.name}</span>
					</div>
				{/each}
			</div>
		</div>

		<!-- UI/UX Design Card -->
		<div
			class="rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-pink-400/50"
		>
			<h3 class="mb-4 flex items-center gap-2 text-xl font-semibold text-pink-400">
				<i class="fa-solid fa-pen-nib"></i>
				UI/UX Design
			</h3>
			<div class="flex flex-wrap gap-2">
				{#each technologies.uidesign as tech}
					<div
						class="flex items-center gap-2 rounded-full bg-white/10 px-3 py-1.5 text-sm shadow transition hover:bg-white/20"
						style="color: {tech.color}"
					>
						{#if tech.icon.startsWith('http') || tech.icon.startsWith('..')}
							<img src={tech.icon.replace('..', '')} alt={tech.name} class="h-4 w-4" />
						{:else if tech.icon.startsWith('<svg')}
							<span class="inline-flex h-4 w-4 items-center">
								{@html tech.icon}
							</span>
						{:else}
							<span class="text-base">{tech.icon}</span>
						{/if}
						<span class="font-medium text-white">{tech.name}</span>
					</div>
				{/each}
			</div>
		</div>

		<!-- Tools Card -->
		<div
			class="rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-gray-400/50"
		>
			<h3 class="mb-4 flex items-center gap-2 text-xl font-semibold text-gray-400">
				<i class="fa-solid fa-wrench"></i>
				Tools
			</h3>
			<div class="flex flex-wrap gap-2">
				{#each technologies.tools as tech}
					<div
						class="flex items-center gap-2 rounded-full bg-white/10 px-3 py-1.5 text-sm shadow transition hover:bg-white/20"
						style="color: {tech.color}"
					>
						{#if tech.icon.startsWith('http') || tech.icon.startsWith('..')}
							<img src={tech.icon.replace('..', '')} alt={tech.name} class="h-4 w-4" />
						{:else if tech.icon.startsWith('<svg')}
							<span class="inline-flex h-4 w-4 items-center">
								{@html tech.icon}
							</span>
						{:else}
							<span class="text-base">{tech.icon}</span>
						{/if}
						<span class="font-medium text-white">{tech.name}</span>
					</div>
				{/each}
			</div>
		</div>
	</div>
</div>

<!-- TIMELINE SECTION -->
<div
	class="mt-3 rounded-md bg-white/5 p-10 shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<h2 class="mb-8 text-3xl font-bold text-white">🏄‍♂️ My Journey</h2>

	<!-- Tab Navigation -->
	<div class="mb-9 flex gap-4 border-b border-white/10 mt-2">
		<button
			class="px-4 py-4 font-semibold transition-all"
			class:text-blue-400={activeTab === 'work'}
			class:text-gray-400={activeTab !== 'work'}
			class:border-b-2={activeTab === 'work'}
			class:border-blue-400={activeTab === 'work'}
			on:click={() => (activeTab = 'work')}
		>
			<i class="fa-solid fa-briefcase mr-2"></i>
			Work Experience
		</button>
		<button
			class="px-4 py-4 font-semibold transition-all"
			class:text-blue-400={activeTab === 'education'}
			class:text-gray-400={activeTab !== 'education'}
			class:border-b-2={activeTab === 'education'}
			class:border-blue-400={activeTab === 'education'}
			on:click={() => (activeTab = 'education')}
		>
			<i class="fa-solid fa-graduation-cap mr-2"></i>
			Education
		</button>
		<button
			class="px-4 py-4 font-semibold transition-all"
			class:text-blue-400={activeTab === 'achievements'}
			class:text-gray-400={activeTab !== 'achievements'}
			class:border-b-2={activeTab === 'achievements'}
			class:border-blue-400={activeTab === 'achievements'}
			on:click={() => (activeTab = 'achievements')}
		>
			<i class="fa-solid fa-trophy mr-2"></i>
			Achievements
		</button>
	</div>

	<!-- Tab Content -->
	<div class="relative">
		<!-- Work Experience -->
		{#if activeTab === 'work'}
			<div class="relative space-y-8">
				{#each filteredExperiences as exp, i}
					{@const colors = getColorClasses(exp.color)}
					<div class="relative flex gap-6 pl-10">
						<!-- Timeline Line -->
						{#if i !== filteredExperiences.length - 1}
							<div class="absolute top-10 left-3.75 h-full w-0.5 bg-white/20"></div>
						{/if}

						<!-- Timeline Dot -->
						<div
							class="absolute top-2 left-0 h-8 w-8 rounded-full {colors.bg} {colors.border} flex items-center justify-center border-2"
						>
							<div class="h-3 w-3 rounded-full {colors.bg}"></div>
						</div>

						<!-- Content Card -->
						<div
							class="flex-1 rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-white/20 hover:bg-white/10"
						>
							<div class="mb-2 flex items-start justify-between">
								<div>
									<h3 class="text-xl font-bold {colors.text}">{exp.position}</h3>
									<p class="text-lg text-white">{exp.company}</p>
									<p class="text-md mt-2 text-white">
										<span class="rounded-full bg-blue-500/70 px-6 py-1">{exp.workingtype}</span>
									</p>
								</div>
								<span class="rounded-full bg-white/10 px-3 py-1 text-sm text-gray-300"
									>{exp.period}</span
								>
							</div>
							<p class="mt-3 text-gray-300">{exp.description}</p>
						</div>
					</div>
				{/each}
			</div>
		{/if}

		<!-- Education -->
		{#if activeTab === 'education'}
			<div class="relative space-y-8">
				{#each education as edu, i}
					{@const colors = getColorClasses(edu.color)}
					<div class="relative flex gap-6 pl-10">
						<!-- Timeline Line -->
						{#if i !== education.length - 1}
							<div class="absolute top-10 left-3.75 h-full w-0.5 bg-white/20"></div>
						{/if}

						<!-- Timeline Dot -->
						<div
							class="absolute top-2 left-0 h-8 w-8 rounded-full {colors.bg} {colors.border} flex items-center justify-center border-2"
						>
							<div class="h-3 w-3 rounded-full {colors.bg}"></div>
						</div>

						<!-- Content Card -->
						<div
							class="flex-1 rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-white/20 hover:bg-white/10"
						>
							<div class="mb-2 flex items-start justify-between">
								<div>
									<h3 class="text-xl font-bold {colors.text}">{edu.degree}</h3>
									<p class="text-lg text-white">{edu.institution}</p>
									{#if edu.gpa}
										<p class="mt-1 text-sm text-gray-400">GPA: {edu.gpa}</p>
									{/if}
								</div>
								<span class="rounded-full bg-white/10 px-3 py-1 text-sm text-gray-300"
									>{edu.period}</span
								>
							</div>
							<p class="mt-3 text-gray-300">{edu.description}</p>
						</div>
					</div>
				{/each}
			</div>
		{/if}

		<!-- Achievements -->
		{#if activeTab === 'achievements'}
			<div class="grid grid-cols-1 gap-6 md:grid-cols-2">
				{#each achievements as achievement}
					{@const colors = getColorClasses(achievement.color)}
					<div
						class="rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-white/20 hover:bg-white/10"
					>
						<div class="mb-4 flex items-start gap-4">
							<div class="flex h-12 w-12 items-center justify-center rounded-full {colors.bg}">
								<i class="{achievement.icon} text-2xl {colors.text}"></i>
							</div>
							<div class="flex-1">
								<h3 class="text-lg font-bold text-white">{achievement.title}</h3>
								<p class="text-sm {colors.text}">{achievement.organization}</p>
								<p class="mt-1 text-xs text-gray-400">{achievement.date}</p>
							</div>
						</div>
						<p class="text-sm text-gray-300">{achievement.description}</p>
					</div>
				{/each}
			</div>
		{/if}
	</div>
</div>

<!-- FEATURED PROJECTS -->
<div
	class="mt-3 rounded-md bg-white/5 p-10 shadow-md backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
	id="projects"
>
	<div class="mb-8 flex items-center justify-between">
		<div class="flex">
			<i class="fa-solid fa-star mr-3 text-2xl text-yellow-400"></i>
			<h2 class="text-2xl font-semibold">Highlighted Works</h2>
		</div>

		<a href="/projects" class="rounded-md bg-blue-950/70 px-7 py-3">See Another Works</a>
	</div>

	<div class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-2">
		{#each selectedProjects as project}
			<div class="rounded-lg bg-white/10 shadow-lg transition hover:bg-white/15">
				<img
					src={project.image}
					alt={project.title}
					class="h-48 w-full rounded-t-lg object-cover"
					loading="lazy"
				/>
				<div class="p-5">
					<h3 class="mb-2 text-xl font-semibold text-white">{project.title}</h3>
					<p class="mb-4 text-sm text-gray-300">{project.description}</p>
					<div class="mb-4 flex flex-wrap gap-2">
						{#each project.tags as tag}
							<span class="rounded bg-white/20 px-2 py-1 text-xs text-white">{tag}</span>
						{/each}
					</div>
					<a
						href={project.link}
						target="_blank"
						class="inline-block rounded bg-blue-600 px-4 py-2 text-sm font-semibold text-white transition hover:bg-blue-700"
					>
						View Project →
					</a>
				</div>
			</div>
		{/each}
	</div>
</div>

<!-- CONTACT SECTION -->
<div
	class="mt-3 rounded-md bg-white/5 p-10 shadow-md backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
	id="contact">

	<h2 class="mb-8 text-3xl font-bold text-white">📬 Get in Touch</h2>
	
	<div class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-2">
		<!-- Contact Info -->
		<div
			class="flex justify-center rounded-md bg-white/5 p-10 shadow-md backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
		>
			<div
				class="flex h-10 w-10 mr-4 shrink-0 items-center justify-center rounded-full border border-blue-400/30 bg-blue-900/70 backdrop-blur-sm sm:h-12 sm:w-12"
			>
				<i class="fa-regular fa-envelope text-lg text-blue-400 sm:text-xl"></i>
			</div>
			<div class="min-w-0 flex-1">
				<h3 class="mb-2 text-base font-semibold text-white sm:text-lg">Email</h3>
				<p class="mb-2 text-xs text-white/70 sm:text-sm">You can contact me via email at:</p>
				<a
					href="mailto:nandanadevadatta161006@gmail.com"
					class="text-sm font-medium break-all text-blue-400 transition-colors hover:text-blue-300 sm:text-base"
				>
					nandanadevadatta161006@gmail.com
				</a>
			</div>
		</div>

		<!-- Contact Info -->
		<div
			class="flex justify-center rounded-md bg-white/5 p-10 shadow-md backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
		>
			<div
				class="flex h-10 w-10 mr-4  shrink-0 items-center justify-center rounded-full border border-purple-400/30 bg-purple-900/70 backdrop-blur-sm sm:h-12 sm:w-12"
			>
				<i class="fa-solid fa-share-nodes text-lg text-purple-400 sm:text-xl"></i>
			</div>
			<div class="min-w-0 flex-1">
				<h3 class="mb-2 text-base font-semibold text-white sm:text-lg">Social Media</h3>
				<p class="mb-4 text-xs text-white/70 sm:text-sm">Or you can connect with me at:</p>
				<a
					href="https://github.com/1610Deva"
					target="_blank"
					rel="noopener noreferrer"
					class="group flex items-center gap-2 my-2 text-white/90 transition-colors hover:text-blue-400 sm:gap-3"
				>
					<i class="fa-brands fa-github text-lg transition-transform group-hover:scale-110 sm:text-xl"
					></i>
					<span class="text-sm sm:text-base">GitHub</span>
				</a>

				<a
					href="https://www.linkedin.com/in/devadattagiri/"
					target="_blank"
					rel="noopener noreferrer"
					class="group flex items-center gap-2 my-2 text-white/90 transition-colors hover:text-blue-400 sm:gap-3"
				>
					<i
						class="fa-brands fa-linkedin text-lg transition-transform group-hover:scale-110 sm:text-xl"
					></i>
					<span class="text-sm sm:text-base">LinkedIn</span>
				</a>

				<a
					href="https://www.instagram.com/@gusdevadatta_/"
					target="_blank"
					rel="noopener noreferrer"
					class="group flex items-center gap-2 my-2 text-white/90 transition-colors hover:text-blue-400 sm:gap-3"
				>
					<i class="fa-brands fa-instagram text-lg transition-transform group-hover:scale-110 sm:text-xl"
					></i>
					<span class="text-sm sm:text-base"> Instagram </span>
				</a>
			</div>
		</div>
	</div>
</div>
