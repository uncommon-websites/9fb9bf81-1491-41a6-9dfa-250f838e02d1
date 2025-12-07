<script lang="ts">
	import { onMount } from 'svelte';

	// Data for the waveform
	const barCount = 60;
	const bars = Array.from({ length: barCount }, (_, i) => {
		const x = i / barCount;
		const baseHeight = 40 + Math.sin(x * Math.PI) * 60;
		const random = Math.random() * 20;
		return Math.max(20, Math.min(100, baseHeight + random));
	});

	// Colors for the middle section of the waveform
	const getBarColor = (i: number) => {
		const total = barCount;
		const startColor = Math.floor(total * 0.25);
		const endColor = Math.floor(total * 0.75);
		
		if (i >= startColor && i <= endColor) {
			// Gradient from Blue to Yellow
			const range = endColor - startColor;
			const pos = (i - startColor) / range;
			
			if (pos < 0.2) return '#1d4ed8'; // Blue
			if (pos < 0.4) return '#7e22ce'; // Purple
			if (pos < 0.6) return '#db2777'; // Pink
			if (pos < 0.8) return '#ea580c'; // Orange
			return '#eab308'; // Yellow
		}
		
		// Alternating black/grey for the rest
		return i % 2 === 0 ? '#111' : '#ccc';
	};
</script>

<div class="w-full overflow-x-hidden bg-[#F3F3EF] text-[#111]">
	<!-- Hero Section -->
	<section class="flex flex-col items-center justify-center pt-20 pb-32 px-6 text-center">
		<!-- Waveform Graphic -->
		<div class="h-24 flex items-end justify-center gap-[2px] mb-12 w-full max-w-3xl mx-auto" aria-hidden="true">
			{#each bars as height, i}
				<div 
					class="w-2 rounded-t-sm rounded-b-sm"
					style="height: {height}%; background-color: {getBarColor(i)};"
				></div>
			{/each}
		</div>

		<h1 class="text-5xl md:text-7xl leading-tight max-w-4xl mx-auto mb-10 font-serif">
			AI is <span class="italic font-normal">meaningful</span> when you<br />
			can naturally interact with it.
		</h1>

		<button class="bg-black text-white px-6 py-3 rounded-full text-sm font-sans font-medium hover:bg-gray-800 transition-colors cursor-pointer">
			Explore datasets
		</button>
	</section>

	<!-- Mission Section -->
	<section class="bg-white py-32 px-6">
		<div class="max-w-4xl mx-auto">
			<p class="text-3xl md:text-4xl leading-snug text-gray-800 font-serif">
				We are an audio data research company.
				<span class="text-gray-400">Our mission is to bring AI into the real world
				through voice, the most important interface to
				human interaction.</span>
			</p>
		</div>
	</section>

	<!-- Process Section -->
	<section class="py-32 px-6 bg-[#F3F3EF]">
		<div class="max-w-6xl mx-auto">
			<div class="flex flex-col items-center mb-16">
				<div class="flex flex-col items-center gap-2 mb-4">
					<div class="w-6 h-6 rounded-full border border-gray-400 flex items-center justify-center text-xs font-sans text-gray-500">2</div>
					<div class="w-px h-8 bg-gray-300"></div>
					<span class="text-xs font-sans uppercase tracking-widest text-gray-500">Process</span>
				</div>
				<h2 class="text-4xl md:text-5xl text-center max-w-2xl font-serif">
					We develop audio datasets with <span class="italic">the<br/>same rigor</span> researchers bring to models.
				</h2>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
				<!-- Steps -->
				<div class="space-y-12 pl-4 md:pl-20">
					<div class="relative">
						<span class="absolute -left-8 top-0 text-xs font-sans text-gray-500">i.</span>
						<h3 class="text-xl font-medium mb-2 font-serif">Hypothesize</h3>
						<p class="text-gray-500 text-sm font-sans max-w-xs leading-relaxed">
							Determine an audio AI capability we wish to unlock.
						</p>
					</div>
					<div class="relative opacity-40">
						<span class="absolute -left-8 top-0 text-xs font-sans">ii.</span>
						<h3 class="text-xl font-medium mb-2 font-serif">Design</h3>
						<p class="text-gray-500 text-sm font-sans max-w-xs leading-relaxed">
							Architect a shape of data to teach models that capability.
						</p>
					</div>
				</div>

				<!-- Graphic -->
				<div class="relative h-96 w-full flex items-center justify-center bg-[#F3F3EF]">
					<div class="relative w-80 h-64">
						<span class="absolute left-0 top-1/2 -translate-y-1/2 -translate-x-12 text-xs font-sans text-gray-500">a.</span>
						<span class="absolute right-0 top-1/2 -translate-y-1/2 translate-x-12 text-xs font-sans text-gray-500">b.</span>
						
						<svg viewBox="0 0 300 200" class="w-full h-full">
							<defs>
								<!-- Pattern of vertical lines -->
								<pattern id="lines" x="0" y="0" width="6" height="200" patternUnits="userSpaceOnUse">
									<rect x="0" y="0" width="3" height="200" fill="currentColor" />
								</pattern>
								
								<!-- Rainbow Gradient -->
								<linearGradient id="rainbow" x1="100" y1="0" x2="200" y2="0" gradientUnits="userSpaceOnUse">
									<stop offset="0%" stop-color="#1d4ed8" />
									<stop offset="25%" stop-color="#7e22ce" />
									<stop offset="50%" stop-color="#db2777" />
									<stop offset="75%" stop-color="#ea580c" />
									<stop offset="100%" stop-color="#eab308" />
								</linearGradient>
								
								<!-- Circle Paths -->
								<circle id="circle-a" cx="110" cy="100" r="60" />
								<circle id="circle-b" cx="190" cy="100" r="60" />
							</defs>
							
							<!-- Left Circle (Black Lines) -->
							<g class="text-black">
								<defs>
									<clipPath id="clip-a-only">
										<use href="#circle-a" />
									</clipPath>
								</defs>
								<rect x="0" y="0" width="300" height="200" fill="url(#lines)" clip-path="url(#clip-a-only)" />
							</g>

							<!-- Right Circle (Black Lines) -->
							<g class="text-black">
								<defs>
									<clipPath id="clip-b-only">
										<use href="#circle-b" />
									</clipPath>
								</defs>
								<rect x="0" y="0" width="300" height="200" fill="url(#lines)" clip-path="url(#clip-b-only)" />
							</g>

							<!-- Intersection (Colored Lines) -->
							<g>
								<defs>
									<clipPath id="clip-both">
										<use href="#circle-a" />
									</clipPath>
									<clipPath id="clip-both-2">
										<use href="#circle-b" />
									</clipPath>
									<pattern id="lines-white" x="0" y="0" width="6" height="200" patternUnits="userSpaceOnUse">
										<rect x="0" y="0" width="3" height="200" fill="white" />
									</pattern>
									<mask id="mask-rainbow">
										<rect x="0" y="0" width="300" height="200" fill="black" />
										<rect x="0" y="0" width="300" height="200" fill="url(#lines-white)" />
									</mask>
								</defs>
								
								<g clip-path="url(#clip-both)">
									<g clip-path="url(#clip-both-2)">
										<rect x="0" y="0" width="300" height="200" fill="url(#rainbow)" mask="url(#mask-rainbow)" />
									</g>
								</g>
							</g>
						</svg>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Usage Section -->
	<section class="bg-white py-32 px-6">
		<div class="max-w-4xl mx-auto">
			<p class="text-3xl md:text-4xl leading-snug text-gray-400 font-serif">
				<span class="text-black">Our datasets are used by Fortune 100 companies
				and research labs</span> that work with speech
				recognition, translation, synthesis, and
				conversational AI.
			</p>
		</div>
	</section>

	<!-- Featured Datasets -->
	<section class="bg-[#1C1C1C] text-white py-32 px-6">
		<div class="max-w-6xl mx-auto">
			<div class="flex flex-col items-start mb-16">
				<div class="flex items-center gap-3 mb-6">
					<div class="w-6 h-6 rounded-full border border-gray-600 flex items-center justify-center text-xs font-sans text-gray-400">3</div>
					<div class="w-12 h-px bg-gray-600"></div>
					<span class="text-xs font-sans uppercase tracking-widest text-gray-400">Featured Datasets</span>
				</div>
				<h2 class="text-4xl md:text-5xl max-w-3xl leading-tight font-serif">
					A dataset suite designed for speech-to-speech,
					multilingual, and voice interaction systems
				</h2>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-2 gap-6">
				<!-- Converse Card -->
				<div class="bg-[#F3F3EF] text-black p-8 rounded-sm h-[500px] flex flex-col relative overflow-hidden group">
					<div class="flex items-center gap-2 mb-4">
						<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z"></path></svg>
						<h3 class="text-2xl font-serif">Converse</h3>
					</div>
					<p class="text-sm font-sans text-gray-600 mb-8 max-w-sm leading-relaxed">
						Our flagship English dataset includes over 15,000 hours of channel-separated, natural two-speaker conversations covering a wide range of topics.
					</p>
					
					<!-- Waveform Visualization -->
					<div class="mt-auto flex flex-col gap-2 opacity-90">
						<!-- Track 1: Dark with white bars -->
						<div class="flex items-center gap-[2px] h-10 bg-[#222] px-2 rounded-sm overflow-hidden">
							{#each Array(50) as _, i}
								<div class="w-[3px] bg-white/90 rounded-full" style="height: {20 + Math.random() * 60}%"></div>
							{/each}
						</div>
						<!-- Track 2: Light with black bars -->
						<div class="flex items-center gap-[2px] h-10 px-2 rounded-sm overflow-hidden">
							<div class="w-8"></div> <!-- Spacer -->
							{#each Array(40) as _, i}
								<div class="w-[3px] bg-black/80 rounded-full" style="height: {20 + Math.random() * 60}%"></div>
							{/each}
						</div>
						<!-- Track 3: Dark with white bars -->
						<div class="flex items-center gap-[2px] h-10 bg-[#222] px-2 rounded-sm overflow-hidden">
							{#each Array(30) as _, i}
								<div class="w-[3px] bg-white/90 rounded-full" style="height: {20 + Math.random() * 60}%"></div>
							{/each}
						</div>
						<!-- Track 4: Light with grey bars -->
						<div class="flex items-center gap-[2px] h-10 px-2 rounded-sm overflow-hidden justify-end">
							{#each Array(45) as _, i}
								<div class="w-[3px] bg-gray-400/50 rounded-full" style="height: {10 + Math.random() * 40}%"></div>
							{/each}
						</div>
					</div>
				</div>

				<!-- Atlas Card -->
				<div class="bg-[#dcdce5] text-black p-8 rounded-sm h-[500px] flex flex-col relative overflow-hidden">
					<div class="flex items-center gap-2 mb-4 z-10">
						<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
						<h3 class="text-2xl font-serif">Atlas</h3>
					</div>
					<p class="text-sm font-sans text-gray-600 mb-8 max-w-sm leading-relaxed z-10">
						A multilingual dataset spanning 15+ languages.
					</p>

					<!-- Map Visual -->
					<div class="absolute inset-0 top-20 opacity-40 pointer-events-none mix-blend-multiply">
						<!-- Better Map SVG -->
						<svg viewBox="0 0 800 400" class="w-full h-full fill-gray-400">
							<path d="M150,100 Q180,80 200,100 T250,120 T300,100 T350,130 V250 H100 V150 Q120,160 150,100 M400,100 Q450,50 500,100 T600,100 T700,150 V300 H400 V100" />
							<!-- Abstract continents -->
						</svg>
					</div>
					
					<div class="absolute bottom-24 left-1/2 -translate-x-1/2 z-20">
						<div class="bg-white/90 backdrop-blur px-8 py-4 rounded-[2rem] shadow-sm border border-white/50">
							<span class="font-sans text-xl font-medium">안녕</span>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- News Section -->
	<section class="bg-white py-32 px-6">
		<div class="max-w-6xl mx-auto">
			<div class="flex items-center gap-3 mb-10">
				<div class="w-6 h-6 rounded-full border border-gray-300 flex items-center justify-center text-xs font-sans text-gray-500">5</div>
				<div class="w-12 h-px bg-gray-200"></div>
				<span class="text-xs font-sans uppercase tracking-widest text-gray-500">News</span>
			</div>

			<div class="flex justify-between items-end mb-12">
				<h2 class="text-4xl md:text-5xl font-serif">Updates on our progress</h2>
				<button class="border border-gray-200 px-4 py-2 rounded-full text-xs font-sans font-medium hover:bg-gray-50 transition-colors cursor-pointer">
					View all
				</button>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-3 gap-8">
				<!-- News Item 1 -->
				<div class="group cursor-pointer">
					<div class="bg-[#F3F3EF] aspect-[4/3] mb-6 relative overflow-hidden border border-gray-100 p-6 flex flex-col justify-between">
						<div class="flex items-center gap-2 text-[10px] font-bold text-gray-400 uppercase tracking-wider">
							<div class="w-2 h-2 bg-gray-300 rounded-sm"></div>
							David AI
						</div>
						
						<!-- Visual: Mini Waveform -->
						<div class="absolute inset-0 flex items-center justify-center opacity-80 pointer-events-none">
							<div class="flex items-end gap-[2px] h-16">
								{#each Array(20) as _, i}
									<div class="w-1.5 bg-gray-800" style="height: {20 + Math.random() * 80}%; background-color: {i > 5 && i < 15 ? ['#1d4ed8', '#7e22ce', '#db2777', '#ea580c', '#eab308'][Math.floor(Math.random()*5)] : '#111'}"></div>
								{/each}
							</div>
						</div>

						<div class="relative z-10">
							<div class="text-4xl font-serif mb-1">$50M</div>
							<div class="text-xs font-sans text-gray-500">Series B Funding</div>
						</div>
						
						<div class="flex justify-between items-end relative z-10">
							<div class="text-[10px] font-sans text-gray-400 font-bold uppercase">Meritech</div>
						</div>
					</div>
					<h3 class="text-xl font-medium mb-2 group-hover:underline decoration-1 underline-offset-4 font-serif">Announcing Our $50M Series B Led by Meritech</h3>
					<p class="text-xs font-sans text-gray-400">Oct 8, 2025 · News</p>
				</div>

				<!-- News Item 2 -->
				<div class="group cursor-pointer">
					<div class="bg-[#F3F3EF] aspect-[4/3] mb-6 relative overflow-hidden border border-gray-100 p-6 flex flex-col justify-between">
						<div class="flex items-center gap-2 text-[10px] font-bold text-gray-400 uppercase tracking-wider">
							<div class="w-2 h-2 bg-gray-300 rounded-sm"></div>
							David AI
						</div>
						
						<div class="absolute inset-0 flex items-center justify-center pointer-events-none">
							<span class="text-6xl font-serif text-gray-900">$25M</span>
						</div>

						<div class="relative z-10 mt-auto">
							<div class="text-xs font-sans text-gray-500">Series A Funding</div>
						</div>
						
						<div class="flex justify-between items-end relative z-10 mt-2">
							<div class="text-[10px] font-sans text-gray-400 font-bold uppercase">Alt Capital</div>
						</div>
					</div>
					<h3 class="text-xl font-medium mb-2 group-hover:underline decoration-1 underline-offset-4 font-serif">Announcing Our $25M Series A Led by Alt Capital</h3>
					<p class="text-xs font-sans text-gray-400">May 22, 2025 · News</p>
				</div>

				<!-- News Item 3 -->
				<div class="group cursor-pointer">
					<div class="bg-[#F3F3EF] aspect-[4/3] mb-6 relative overflow-hidden border border-gray-100 p-6 flex flex-col justify-between">
						<div class="flex items-center gap-2 text-[10px] font-bold text-gray-400 uppercase tracking-wider">
							<div class="w-2 h-2 bg-gray-300 rounded-sm"></div>
							David AI
						</div>
						
						<!-- Visual: Seal -->
						<div class="absolute inset-0 flex items-center justify-center pointer-events-none opacity-10">
							<div class="w-32 h-32 rounded-full border-4 border-black flex items-center justify-center">
								<div class="w-24 h-24 rounded-full border-2 border-black"></div>
							</div>
						</div>
						
						<div class="relative z-10 flex flex-col justify-center h-full">
							<div class="text-4xl font-serif mb-1">$5M</div>
							<div class="text-xs font-sans text-gray-500">Seed Funding</div>
						</div>
						
						<div class="flex justify-between items-end relative z-10">
							<div class="text-[10px] font-sans text-gray-400 font-bold uppercase">First Round</div>
						</div>
					</div>
					<h3 class="text-xl font-medium mb-2 group-hover:underline decoration-1 underline-offset-4 font-serif">Announcing Our $5M Seed Round Led by First Round</h3>
					<p class="text-xs font-sans text-gray-400">Jan 16, 2025 · News</p>
				</div>
			</div>
		</div>
	</section>

	<!-- Footer -->
	<section class="bg-[#F3F3EF] py-32 px-6">
		<div class="max-w-6xl mx-auto flex flex-col items-center text-center mb-32">
			<h2 class="text-4xl md:text-6xl mb-10 max-w-2xl font-serif">Interested in working with us?</h2>
			<div class="flex gap-4">
				<button class="border border-gray-300 px-6 py-3 rounded-full text-sm font-sans font-medium hover:bg-white transition-colors cursor-pointer">
					Contact us
				</button>
				<button class="bg-black text-white px-6 py-3 rounded-full text-sm font-sans font-medium hover:bg-gray-800 transition-colors cursor-pointer">
					See open roles
				</button>
			</div>
		</div>

		<div class="max-w-6xl mx-auto flex flex-col md:flex-row justify-between items-center text-xs font-sans text-gray-500 border-t border-gray-200 pt-8">
			<p>© 2025 David AI Labs, Inc. All rights reserved.</p>
			<div class="flex gap-6 mt-4 md:mt-0">
				<a href="#" class="hover:text-black">Terms of service</a>
				<a href="#" class="hover:text-black">Privacy policy</a>
			</div>
			<div class="flex gap-4 mt-4 md:mt-0">
				<a href="#" class="hover:text-black" aria-label="LinkedIn">
					<svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
				</a>
				<a href="#" class="hover:text-black" aria-label="X">
					<svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg>
				</a>
			</div>
		</div>
	</section>
</div>

<style>
	/* Ensure fonts are applied if Tailwind classes miss */
	:global(body) {
		font-family: 'EB Garamond', serif;
	}
</style>

