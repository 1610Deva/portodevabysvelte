<script lang="ts">
	import { onMount } from 'svelte';

	interface Project {
		title: string;
		description: string;
		link: string;
		image: string;
		tags: string[];
		featured?: boolean;
	}

	let projects: Project[] = [];
	let filteredProjects: Project[] = [];
	let selectedTag: string = 'All';
	let allTags: string[] = [];
	let isVisible = false;

	onMount(async () => {
		isVisible = true;
		const res = await fetch('/data/data.json');
		const data = await res.json();
		projects = data.projects;
		filteredProjects = projects;

		const tagsSet = new Set<string>();
		projects.forEach((project) => {
			project.tags.forEach((tag) => tagsSet.add(tag));
		});
		allTags = ['All', ...Array.from(tagsSet).sort()];
	});

	function filterProjects(tag: string) {
		selectedTag = tag;
		if (tag === 'All') {
			filteredProjects = projects;
		} else {
			filteredProjects = projects.filter((project) => project.tags.includes(tag));
		}
	}
</script>

<svelte:head>
	<title>Projects - Devadatta Giri</title>
</svelte:head>

<!-- HEADER SECTION -->
<div
	class="mt-3 rounded-md bg-white/5 p-10 shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<div class="text-center">
		<h1 class="mb-4 text-4xl font-bold text-white">
			<i class="fa-solid fa-folder-open mr-3 text-blue-400"></i>
			My Projects
		</h1>
		<p class="mx-auto max-w-2xl text-lg text-gray-300">
			A collection of projects I've worked on, ranging from web development to UI/UX design.
			Each project represents a unique challenge and learning experience.
		</p>
	</div>
</div>

<!-- FILTER SECTION -->
<div
	class="mt-3 rounded-md bg-white/5 p-6 shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<div class="mb-2 text-center">
		<h3 class="mb-4 text-lg font-semibold text-white">
			<i class="fa-solid fa-filter mr-2"></i>
			Filter by Technology
		</h3>
		<div class="flex flex-wrap justify-center gap-2">
			{#each allTags as tag}
				<button
					class="rounded-full px-4 py-2 text-sm font-medium transition-all"
					class:bg-blue-600={selectedTag === tag}
					class:text-white={selectedTag === tag}
					class:bg-white={selectedTag !== tag}
					class:text-black={selectedTag !== tag}
					class:hover:bg-white={selectedTag !== tag}
					on:click={() => filterProjects(tag)}
				>
					{tag}
				</button>
			{/each}
		</div>
	</div>
</div>

<!-- PROJECTS GRID -->
<div
	class="mt-3 rounded-md bg-white/5 p-10 shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<div class="mb-6 flex items-center justify-between">
		<h2 class="text-2xl font-semibold text-white">
			{selectedTag === 'All' ? 'All Projects' : `${selectedTag} Projects`}
			<span class="ml-2 text-lg text-gray-400">({filteredProjects.length})</span>
		</h2>
	</div>

	{#if filteredProjects.length === 0}
		<div class="py-20 text-center">
			<i class="fa-solid fa-folder-open text-6xl text-gray-500"></i>
			<p class="mt-4 text-xl text-gray-400">No projects found with this filter</p>
		</div>
	{:else}
		<div class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-3">
			{#each filteredProjects as project}
				<div
					class="group rounded-lg bg-white/10 shadow-lg transition-all duration-300 hover:-translate-y-2 hover:bg-white/15 hover:shadow-xl"
				>
					<div class="relative overflow-hidden rounded-t-lg">
						<img
							src={project.image}
							alt={project.title}
							class="h-48 w-full object-cover transition-transform duration-300 group-hover:scale-110"
							loading="lazy"
						/>
						{#if project.featured}
							<div
								class="absolute right-2 top-2 rounded-full bg-yellow-500/90 px-3 py-1 text-xs font-semibold text-white"
							>
								<i class="fa-solid fa-star mr-1"></i>
								Featured
							</div>
						{/if}
					</div>
					<div class="p-5">
						<h3 class="mb-2 text-xl font-semibold text-white">{project.title}</h3>
						<p class="mb-4 text-sm text-gray-300">{project.description}</p>
						<div class="mb-4 flex flex-wrap gap-2">
							{#each project.tags as tag}
								<span
									class="cursor-pointer rounded bg-white/20 px-2 py-1 text-xs text-white transition hover:bg-blue-600"
									on:click={() => filterProjects(tag)}
								>
									{tag}
								</span>
							{/each}
						</div>
						<a
							href={project.link}
							target="_blank"
							class="inline-flex items-center gap-2 rounded bg-blue-600 px-4 py-2 text-sm font-semibold text-white transition hover:bg-blue-700"
						>
							View Project
							<i class="fa-solid fa-arrow-right"></i>
						</a>
					</div>
				</div>
			{/each}
		</div>
	{/if}
</div>

<!-- BACK TO HOME -->
<div
	class="mt-3 rounded-md bg-white/5 p-6 text-center shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<a
		href="/"
		class="inline-flex items-center gap-2 rounded border border-white px-6 py-3 text-white transition hover:border-blue-600 hover:bg-blue-600"
	>
		<i class="fa-solid fa-arrow-left"></i>
		Back to Home
	</a>
</div>

