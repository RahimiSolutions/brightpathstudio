<script lang="ts">
	import { dev } from '$app/environment';
	import { language, locale } from '$lib/text/i18n';
	import { onMount } from 'svelte';

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
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<!-- <link
		href="https://fonts.googleapis.com/css2?family=Anybody:wght@100..900&family=Quicksand:wght@300..700&display=swap"
		rel="stylesheet"
	/> -->

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

<slot />

<style>
	:global(*) {
		--white: #fefefe;
		--primary: #f8de7e;
		--secondary: #fbedb7;
		--bg-light: rgb(250, 250, 250);
		--bg-dark: #080a16;
		/* --bg-dark: #0d0f0f; */
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		scroll-behavior: smooth;
	}
	:global(body) {
		background-color: var(--bg-light);
	}
</style>
