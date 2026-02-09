<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/img/favico.ico';

	let { children } = $props();

	import { onMount } from 'svelte';

	let isOpen = $state(false);
	let isScrolled = $state(false);

	const navItems = [
		{ label: 'About', href: '/about' },
		{ label: 'Projects', href: '/projects' },
		{ label: 'Contact', href: '/#contact' }
	];

	onMount(() => {
		const handleScroll = () => {
			isScrolled = window.scrollY > 50;
		};

		window.addEventListener('scroll', handleScroll);

		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
	});

	const toggleMenu = () => {
		isOpen = !isOpen;
	};

	const closeMenu = () => {
		isOpen = false;
	};
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<div>
	<!-- Navbar -->
	<nav
		class={`sticky top-0 z-50 w-full border-b border-gray-700 transition-all duration-300 ${
			isScrolled ? 'bg-slate-950/85 backdrop-blur-xs' : 'bg-slate-950'
		}`}
	>
		<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<div class="flex h-20 items-center justify-between">
				<!-- Logo -->
				<div class="shrink-0">
					<a href="/" class="md:text-3xl font-bold text-white md:-ml-8 text-2xl">PortoDeva</a>
				</div>

				<!-- Desktop Menu -->
				<ul class="hidden items-center space-x-2 md:flex">
					<li>
						<a href="https://www.linkedin.com/in/devadattagiri/" target="_blank" aria-label="Linkedin Deva" class="sm:text-sm text-lg font-medium mr-3">
							<i class="fa-brands fa-linkedin text-2xl mr-2" style="color: #ffffff;"></i>Linkedin
						</a>
					</li>
					<li>
						<a href="https://github.com/1610Deva" target="_blank" aria-label="Github Deva" class="sm:text-sm text-lg font-medium px-2 py-1">
							<i class="fa-brands fa-github text-2xl mr-2" style="color: #ffffff;"></i>Github
						</a>
					</li>
					{#each navItems as item}
						<li>
							<a
								href={item.href}
								class="rounded px-4 py-2 text-lg font-medium text-gray-300 transition-colors duration-200 hover:bg-white/10 hover:text-white"
							>
								{item.label}
							</a>
						</li>
					{/each}
				</ul>

				<!-- Hamburger Menu (Mobile) -->
				<div class="md:hidden">
					<button
						onclick={toggleMenu}
						class="inline-flex items-center justify-center rounded-md p-2 text-gray-300 transition-colors duration-200 hover:bg-slate-800 hover:text-white"
					>
						<svg
							class={`h-6 w-6 transition-transform duration-300 ${isOpen ? 'rotate-90' : ''}`}
							fill="none"
							stroke="currentColor"
							viewBox="0 0 24 24"
						>
							{#if !isOpen}
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M4 6h16M4 12h16M4 18h16"
								/>
							{:else}
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M6 18L18 6M6 6l12 12"
								/>
							{/if}
						</svg>
					</button>
				</div>
			</div>

			<!-- Mobile Menu - Hamburger open -->
			{#if isOpen}
				<div
					class="animate-in slide-in-from-top-2 border-t border-gray-700  duration-200 md:hidden py-3"
				>
					<div class="space-y-1 px-2 pt-2 pb-3">
						{#each navItems as item}
							<a
								href={item.href}
								onclick={closeMenu}
								class="block rounded-md px-3 py-2 text-base font-medium text-gray-300 transition-colors duration-200 hover:bg-slate-800 hover:text-white"
							>
								{item.label}
							</a>
						{/each}
					</div>
					<div class="px-2 py-3">
						<button
							class="w-full rounded bg-white px-4 py-2 font-medium text-slate-950 transition-colors duration-200 hover:bg-gray-100"
						>
							Reach Me!
						</button>
					</div>

					<div class="flex items-center gap-3 ml-5 mt-4">
						<h3 class="block text-lg font-medium">Let's Connect 👉🏻</h3>
						<a href="https://www.linkedin.com/in/devadattagiri/" target="_blank" aria-label="Linkedin Deva" class="sm:text-sm text-base font-medium px-2 py-1">
							<i class="fa-brands fa-linkedin text-2xl" style="color: #ffffff;"></i>
						</a>
						<a href="https://github.com/devadattagiri" target="_blank" aria-label="Github Deva" class="sm:text-sm text-base font-medium px-2 py-1">
							<i class="fa-brands fa-github text-2xl" style="color: #ffffff;"></i>
						</a>
					</div>
					
				</div>
			{/if}
		</div>
	</nav>

	<main class="container mx-auto px-4 py-8">
		{@render children()}
	</main>

	<!-- Footer -->
	<footer class="text-center pt-3 pb-4 border-t border-gray-700 text-gray-400 text-sm">
		<span>
			© {new Date().getFullYear()} Devadatta Giri. All rights reserved. <br>
		</span>
	</footer>
</div>
