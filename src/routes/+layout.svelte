<script lang="ts">
	import { dev } from '$app/environment';
    import '../lib/styles/fonts.css';
	import { language, locale } from '$lib/text/i18n';
	import { onMount } from 'svelte';
	import Navbar from '../components/navbar/Navbar.svelte';
	import MobileFooter from '../components/footer/MobileFooter.svelte';
	import Mobilenavbar from '../components/navbar/MobileNavbar.svelte';

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
<Mobilenavbar/>
<slot />

<style>
	
	:global(*) {
		--blue-400: rgb(120, 174, 255);
		--blue-500: #4D93FB;
		--blue-600: #3D86F3;
		--white: #fdfdfd;
		--black: #2a2a2a;
		--grey: #5d5d5d;

        --fs-400: 1rem;
        --fs-500: 1.25rem;
        --fs-600: 1.5rem;
        --fs-700: 2rem;
        --fs-800: 2.5rem;
        --fs-900: 2.75rem;
		/* --bg-dark: #0d0f0f; */
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		scroll-behavior: smooth;
	}
	:global(body) {
		background-color: var(--white);
	}
	
</style>
