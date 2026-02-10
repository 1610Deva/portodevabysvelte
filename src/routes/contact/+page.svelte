<script lang="ts">
	import { onMount } from 'svelte';

	let isVisible = false;

	onMount(() => {
		setTimeout(() => {
            isVisible = true;
        }, 200);
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
	<title>Contact Me - PortoDevadatta</title>
</svelte:head>

<!-- Header Section -->
<div
	class="mt-3 rounded-md bg-white/5 p-10 shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<h1 class="mb-4 text-4xl font-bold text-white">Get in Touch 📬</h1>
	<p class="text-lg text-gray-300">
		Feel free to reach out to me via email or connect with me on social media.
I'm always open to discussing new projects, creative ideas, or opportunities to be part of your visions.
	</p>
</div>

<!-- Contact Information Section -->
<div
	class="mt-3 rounded-md bg-white/5 p-10 shadow-lg backdrop-blur-xs transition-opacity duration-1000 ease-in-out"
	class:opacity-0={!isVisible}
	class:opacity-100={isVisible}
>
	<h2 class="mb-8 text-2xl font-bold text-white">Contact Info</h2>

	<div class="grid grid-cols-1 gap-6 md:grid-cols-2">
		<!-- Email Card -->
		<div
			class="flex gap-4 rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-blue-400/50 hover:bg-white/10"
		>
			<div
				class="flex h-12 w-12 shrink-0 items-center justify-center rounded-full border border-blue-400/30 bg-blue-900/70 backdrop-blur-sm"
			>
				<i class="fa-regular fa-envelope text-lg text-blue-400"></i>
			</div>
			<div class="min-w-0 flex-1">
				<h3 class="font-semibold text-white">Email</h3>
				<a
					href="mailto:nandanadevadatta161006@gmail.com"
					class="mt-1 break-all text-sm text-blue-400 transition-colors hover:text-blue-300"
				>
					nandanadevadatta161006@gmail.com
				</a>
			</div>
		</div>

		<!-- Location Card -->
		<div
			class="flex gap-4 rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-pink-400/50 hover:bg-white/10"
		>
			<div
				class="flex h-12 w-12 shrink-0 items-center justify-center rounded-full border border-pink-400/30 bg-pink-900/70 backdrop-blur-sm"
			>
				<i class="fa-solid fa-location-dot text-lg text-pink-400"></i>
			</div>
			<div class="min-w-0 flex-1">
				<h3 class="font-semibold text-white">Location</h3>
				<p class="mt-1 text-sm text-gray-400">Surabaya, Indonesia</p>
			</div>
		</div>

		<!-- Social Media Card -->
		<div
			class="rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-purple-400/50 hover:bg-white/10"
		>
			<div class="flex items-center gap-2 mb-4">
				<i class="fa-solid fa-share-nodes text-lg text-purple-400"></i>
				<h3 class="font-semibold text-white">Follow Me</h3>
			</div>
			<div class="space-y-3">
				<a
					href="https://github.com/1610Deva"
					target="_blank"
					rel="noopener noreferrer"
					class="group flex items-center gap-2 text-gray-300 transition-colors hover:text-blue-400"
				>
					<i class="fa-brands fa-github text-lg transition-transform group-hover:scale-110"></i>
					<span class="text-sm">GitHub</span>
				</a>

				<a
					href="https://www.linkedin.com/in/devadattagiri/"
					target="_blank"
					rel="noopener noreferrer"
					class="group flex items-center gap-2 text-gray-300 transition-colors hover:text-blue-400"
				>
					<i
						class="fa-brands fa-linkedin text-lg transition-transform group-hover:scale-110"
					></i>
					<span class="text-sm">LinkedIn</span>
				</a>

				<a
					href="https://www.instagram.com/@gusdevadatta_/"
					target="_blank"
					rel="noopener noreferrer"
					class="group flex items-center gap-2 text-gray-300 transition-colors hover:text-blue-400"
				>
					<i class="fa-brands fa-instagram text-lg transition-transform group-hover:scale-110"></i>
					<span class="text-sm">Instagram</span>
				</a>
			</div>
		</div>

		<!-- Response Time Card -->
		<div
			class="flex gap-4 rounded-lg border border-white/10 bg-white/5 p-6 transition-all hover:border-yellow-400/50 hover:bg-white/10"
		>
			<div
				class="flex h-12 w-12 shrink-0 items-center justify-center rounded-full border border-yellow-400/30 bg-yellow-900/70 backdrop-blur-sm"
			>
				<i class="fa-regular fa-clock text-lg text-yellow-400"></i>
			</div>
			<div class="min-w-0 flex-1">
				<h3 class="font-semibold text-white">Response Time</h3>
				<p class="mt-1 text-sm text-gray-400">I'll try to respond within 24 hours</p>
			</div>
		</div>
	</div>
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
        <i class="fa-solid fa-home"></i>
        Back to Home
    </a>    
</div>
