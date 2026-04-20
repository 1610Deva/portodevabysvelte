<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let { 
		minSize = 1, 
		maxSize = 2,
		speed = 5,
		mobileCount = 70,
		desktopCount = 200
	} = $props();

	let canvas: HTMLCanvasElement;
	let animId: number;

	onMount(() => {
		const ctx = canvas.getContext('2d')!;

		const isMobile = window.innerWidth < 768;
		const STAR_COUNT = isMobile ? mobileCount : desktopCount;

		const resize = () => {
			canvas.width = window.innerWidth;
			canvas.height = document.documentElement.scrollHeight;
		};
		resize();

		type Star = { x: number; y: number; r: number; vx: number; vy: number; alpha: number };
		const stars: Star[] = Array.from({ length: STAR_COUNT }, () => ({
			x: Math.random() * canvas.width,
			y: Math.random() * canvas.height,
			r: Math.random() * (maxSize - minSize) + minSize,          
			vx: (Math.random() - 0.5) * speed,    
			vy: (Math.random() - 0.5) * speed,      
			alpha: Math.random() * 0.6 + 0.3        
		}));

		// Loop animasi
		const draw = () => {
			ctx.clearRect(0, 0, canvas.width, canvas.height);

			for (const s of stars) {
				s.x += s.vx;
				s.y += s.vy;

				if (s.x < 0) s.x = canvas.width;
				if (s.x > canvas.width) s.x = 0;
				if (s.y < 0) s.y = canvas.height;
				if (s.y > canvas.height) s.y = 0;

				ctx.beginPath();
				ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
				ctx.fillStyle = `rgba(255, 255, 255, ${s.alpha})`;
				ctx.fill();
			}

			animId = requestAnimationFrame(draw);
		};

		draw();

		// Resize handler
		let resizeTimer: ReturnType<typeof setTimeout>;
		const onResize = () => {
			clearTimeout(resizeTimer);
			resizeTimer = setTimeout(resize, 200);
		};
		window.addEventListener('resize', onResize, { passive: true });

		return () => {
			window.removeEventListener('resize', onResize);
		};
	});

	onDestroy(() => {
		if (animId) cancelAnimationFrame(animId);
	});
</script>

<canvas
	bind:this={canvas}
	class="fixed inset-0 z-[-1]"
	style="pointer-events: none; will-change: transform;"
	aria-hidden="true"
></canvas>
