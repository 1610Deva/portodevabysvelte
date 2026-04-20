<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/img/favico.ico';
	import StarField from '$lib/components/StarField.svelte';

	let { children } = $props();

	import { onMount } from 'svelte';

	let isOpen = $state(false);
	let isScrolled = $state(false);

	const navItems = [
		{ label: 'About', href: '/about' },
		{ label: 'Projects', href: '/projects' },
		{ label: 'Contact', href: '/contact' }
	];

	onMount(() => {
		const handleScroll = () => {
			isScrolled = window.scrollY > 50;
		};

		window.addEventListener('scroll', handleScroll, { passive: true });

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

<div class="relative">
	<StarField />

	<!-- Navbar -->
	<nav
		class={`sticky top-0 z-50 w-full border-b border-gray-700 transition-all duration-300 ${
			isScrolled ? 'bg-slate-950 shadow-lg shadow-black/30' : 'bg-slate-950'
		}`}
	>
		<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<div class="flex h-16 items-center justify-between">
				<!-- Logo -->
				<div class="shrink-0">
					<a href="/" class="text-2xl font-bold text-white">DevaDev</a>
				</div>

				<!-- Desktop Menu -->
				<ul class="hidden items-center space-x-2 md:flex">
					<li>
						<a href="https://www.linkedin.com/in/devadattagiri/" target="_blank" aria-label="Linkedin Deva" class="text-lg font-medium mr-3 text-gray-300 transition hover:text-white">
							<i class="fa-brands fa-linkedin text-2xl mr-2" style="color: #ffffff;"></i>Linkedin
						</a>
					</li>
					<li>
						<a href="https://github.com/1610Deva" target="_blank" aria-label="Github Deva" class="text-lg font-medium px-2 py-1 text-gray-300 transition hover:text-white">
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

				<!-- Hamburger Button (Mobile) -->
				<button
					class="md:hidden flex h-10 w-10 items-center justify-center rounded-lg text-gray-300 transition-colors hover:bg-slate-800 hover:text-white"
					onclick={toggleMenu}
					aria-label="Toggle menu"
					aria-expanded={isOpen}
				>
					<span class="relative flex h-5 w-5 flex-col justify-between">
						<span
							class="block h-0.5 w-full rounded-full bg-current transition-all duration-300"
							style={isOpen ? 'transform: translateY(9px) rotate(45deg)' : ''}
						></span>
						<span
							class="block h-0.5 w-full rounded-full bg-current transition-all duration-300"
							style={isOpen ? 'opacity: 0; transform: scaleX(0)' : ''}
						></span>
						<span
							class="block h-0.5 w-full rounded-full bg-current transition-all duration-300"
							style={isOpen ? 'transform: translateY(-9px) rotate(-45deg)' : ''}
						></span>
					</span>
				</button>
			</div>
		</div>
	</nav>

	<!-- Mobile Menu Overlay Backdrop -->
	<div
		class="fixed inset-0 z-40 bg-black/50 transition-opacity duration-300 md:hidden"
		style={isOpen ? 'opacity: 1; pointer-events: auto;' : 'opacity: 0; pointer-events: none;'}
		onclick={closeMenu}
	></div>

	<div
		class="fixed inset-y-0 right-0 z-50 w-72 bg-slate-900 shadow-2xl shadow-black/50 transition-transform duration-300 md:hidden"
		style={isOpen ? 'transform: translateX(0)' : 'transform: translateX(100%)'}
	>
		<!-- Panel Header -->
		<div class="flex h-16 items-center justify-between border-b border-white/10 px-5">
			<span class="text-lg font-bold text-white">Menu</span>
			<button
				class="flex h-9 w-9 items-center justify-center rounded-lg text-gray-400 transition-colors hover:bg-slate-800 hover:text-white"
				onclick={closeMenu}
				aria-label="Close menu"
			>
				<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
				</svg>
			</button>
		</div>

		<!-- Nav Links -->
		<nav class="flex flex-col gap-1 p-4">
			{#each navItems as item}
				<a
					href={item.href}
					onclick={closeMenu}
					class="flex items-center gap-3 rounded-lg px-4 py-3 text-base font-medium text-gray-300 transition-colors hover:bg-slate-800 hover:text-white"
				>
					{item.label}
				</a>
			{/each}
		</nav>

		<!-- Divider -->
		<div class="mx-4 border-t border-white/10"></div>

		<!-- Social Links -->
		<div class="p-4">
			<p class="mb-3 px-1 text-xs font-semibold uppercase tracking-widest text-gray-500">Connect</p>
			<div class="flex flex-col gap-1">
				<a
					href="https://www.linkedin.com/in/devadattagiri/"
					target="_blank"
					rel="noopener noreferrer"
					class="flex items-center gap-3 rounded-lg px-4 py-3 text-sm font-medium text-gray-300 transition-colors hover:bg-slate-800 hover:text-white"
				>
					<i class="fa-brands fa-linkedin text-xl text-blue-400"></i>
					LinkedIn
				</a>
				<a
					href="https://github.com/1610Deva"
					target="_blank"
					rel="noopener noreferrer"
					class="flex items-center gap-3 rounded-lg px-4 py-3 text-sm font-medium text-gray-300 transition-colors hover:bg-slate-800 hover:text-white"
				>
					<i class="fa-brands fa-github text-xl text-white"></i>
					GitHub
				</a>
				<a
					href="https://www.instagram.com/gusdevadatta_/"
					target="_blank"
					rel="noopener noreferrer"
					class="flex items-center gap-3 rounded-lg px-4 py-3 text-sm font-medium text-gray-300 transition-colors hover:bg-slate-800 hover:text-white"
				>
					<i class="fa-brands fa-instagram text-xl text-pink-400"></i>
					Instagram
				</a>
			</div>
		</div>

		<!-- CTA -->
		<div class="absolute bottom-6 left-0 right-0 px-4">
			<a
				href="/contact"
				onclick={closeMenu}
				class="flex w-full items-center justify-center gap-2 rounded-lg bg-blue-600 px-4 py-3 text-sm font-semibold text-white transition-colors hover:bg-blue-700"
			>
				<i class="fa-solid fa-paper-plane"></i>
				Reach Me!
			</a>
		</div>
	</div>

	<main>
		{@render children()}
	</main>

	<!-- Footer -->
	<footer class="text-center pt-3 pb-4 border-t border-gray-700 text-gray-400 text-sm">
		<span>
			© {new Date().getFullYear()} Devadatta Giri. <br>
		</span>
	</footer>
</div>
