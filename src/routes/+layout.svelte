<script lang="ts">
	import { dev } from '$app/environment';
	import '../lib/styles/fonts.css';
	import { language, locale } from '$lib/text/i18n';
	import { onMount } from 'svelte';
	import Navbar from '../components/navbar/Navbar.svelte';
	import MobileFooter from '../components/footer/MobileFooter.svelte';
	import Mobilenavbar from '../components/navbar/MobileNavbar.svelte';
	import Footer from '../components/footer/Footer.svelte';
	import { injectAnalytics } from '@vercel/analytics/sveltekit';
	import { inject } from '@vercel/analytics';
	inject({ mode: dev ? 'development' : 'production' });

	var userLang = navigator.language;
	// nb-NO

	function setLanguage() {
		if (userLang === 'nb-NO' || userLang === 'no' || userLang === 'nn') {
			$language = 'no';
			$locale = 'no';
		} else {
			$language = 'en';
			$locale = 'en';
		}
	}

	onMount(() => {
		userLang = navigator.language || 'en'; // Default to 'en' if navigator.language is not defined.
		setLanguage();
	});
</script>

<svelte:head>
	<title>Brightpath Studio | Styrker bedrifter med alt-i-ett digitale løsninger</title>
	<meta
		name="description"
		content="Brightpath Studio forenkler digital drift for små og mellomstore bedrifter med vår omfattende alt-i-ett plattform. Effektiviser din nettilstedeværelse og øk produktiviteten."
	/>
	<meta name="viewport" content="width=device-width, initial-scale=1" />
	<meta name="robots" content="index, follow" />
	<meta name="content-language" content="no" />
	<meta
		name="keywords"
		content="alt-i-ett plattform, digitale løsninger, bedriftseffektivitet, CRM, kommunikasjonsverktøy, salgsadministrasjon, små bedrifter, mellomstore bedrifter"
	/>
	<meta property="og:title" content="Brightpath Studio | Forenkler digital drift" />
	<meta
		property="og:description"
		content="Styrk din bedrift med Brightpath Studios alt-i-ett digitale plattform. Effektiviser driften og forbedre din nettilstedeværelse enkelt."
	/>
	<meta property="og:type" content="website" />
	<meta property="og:url" content="https://www.brightpath.studio" />
	<!-- <meta property="og:image" content="https://www.brightpath.studio/images/og-image.jpg" /> -->
	<link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
	<link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png" />
	<link rel="icon" type="image/png" sizes="192x192" href="/favicon-192x192.png" />
	<link rel="icon" type="image/svg+xml" href="/favicon.svg" />
</svelte:head>

<Navbar />
<Mobilenavbar />
<slot />
<Footer />
<MobileFooter />

<style>
	:global(*) {
		--blue-200: rgba(120, 174, 255, 0.15);
		--blue-300: rgba(120, 174, 255, 0.25);
		--blue-400: rgb(120, 174, 255);
		--blue-500: #4d93fb;
		--blue-600: #3d86f3;
		--blue-700: #124fa9;
		--blue-800: #11416e;
		--white: #fdfdfd;
		--black: #2a2a2a;
		--grey: #5d5d5d;
		--red: #9c0000;
		--green: #08b90e;

		/* Smallest size, suitable for small print or tags */
		--fs-300: clamp(0.8rem, 0.5826rem + 0.3478vw, 1rem);
		--mfs-300: clamp(0.625rem, 0.5415rem + 0.3339vw, 0.75rem);

		/* Small text, good for body copy or less emphasized text */
		--fs-400: clamp(0.8rem, 0.7283rem + 0.4348vw, 1.25rem);
		--mfs-350: clamp(0.75rem, 0.5831rem + 0.6678vw, 1rem);
		--mfs-400: clamp(1rem, 0.8331rem + 0.6678vw, 1.25rem);

		/* Medium text, good for body copy or subtitles */
		--fs-500: clamp(1rem, 0.7283rem + 0.4348vw, 1.25rem);
		--mfs-500: clamp(1.25rem, 1.0831rem + 0.6678vw, 1.5rem);

		/* Large text, good for subtitles or small headings */
		--fs-600: clamp(1.25rem, 0.9783rem + 0.4348vw, 1.5rem);
		--mfs-600: clamp(2rem, 1.8331rem + 0.6678vw, 2.25rem);

		/* Extra large, good for titles */
		--fs-700: clamp(1.5rem, -0.6304rem + 2.6087vw, 2.5rem);

		/* 2X large, good for main headings */
		--fs-800: clamp(2rem, -0.1739rem + 3.4783vw, 4rem);

		/* 3X large, good for hero text or very large titles */
		--fs-900: clamp(2.5rem, -1.2174rem + 4.3478vw, 4rem);

		margin: 0;
		padding: 0;
		box-sizing: border-box;
		scroll-behavior: smooth;
	}
	:global(body) {
		background-color: var(--white);
	}
</style>
