<script lang="ts">
	import { onMount } from 'svelte';
	import { get } from 'svelte/store';
	import { language, locale } from '$lib/text/i18n';
	import { quintOut } from 'svelte/easing';
	import { slide } from 'svelte/transition';
	import MediaQuery from './MediaQuery.svelte';
	import Globe from '$lib/icons/globe.svelte';

	let isLanguagePickerOpen = false;
	let currentLanguage: string;
	let availableLanguages = [
		{ code: 'en', label: 'English' },
		{ code: 'no', label: 'Norsk' }
	];

	onMount(() => {
		currentLanguage = get(language);
		language.subscribe((value) => {
			currentLanguage = value;
		});
	});

	function toggleLanguagePicker() {
		isLanguagePickerOpen = !isLanguagePickerOpen;
	}

	function selectLanguage(lang: string) {
		if (currentLanguage !== lang) {
			language.set(lang);
			setTimeout(() => {
				locale.set(lang);
			}, 300);
		}
		isLanguagePickerOpen = false;
	}
</script>

<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-static-element-interactions -->
<MediaQuery query="(min-width: 1000px)" let:matches>
	{#if matches}
		<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-static-element-interactions -->
		<div class="language-picker">
			<div class="selected-language" on:click={toggleLanguagePicker}>
				<Globe width="26" />
				<span class="language">{$locale === 'en' ? 'En' : 'No'}</span>
			</div>
			{#if isLanguagePickerOpen}
				<div
					class="dropdown"
					transition:slide={{ delay: 0, duration: 300, easing: quintOut, axis: 'y' }}
				>
					{#each availableLanguages as lang}
						<div class="dropdown-item" on:click={() => selectLanguage(lang.code)}>
							{lang.label}
						</div>
					{/each}
				</div>
			{/if}
		</div>
	{/if}
</MediaQuery>
<MediaQuery query="(max-width: 999px)" let:matches>
	{#if matches}
		<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-static-element-interactions -->
		<div class="mobile-language-picker">
			<div class="selected-language" on:click={toggleLanguagePicker}>
				<Globe width="26" />
				<span class="language">{$locale === 'en' ? 'English' : 'Norsk'}</span>
			</div>
			{#if isLanguagePickerOpen}
				<div
					class="dropdown"
					transition:slide={{ delay: 0, duration: 300, easing: quintOut, axis: 'y' }}
				>
					{#each availableLanguages as lang}
						<div class="dropdown-item" on:click={() => selectLanguage(lang.code)}>
							{lang.label}
						</div>
					{/each}
				</div>
			{/if}
		</div>
	{/if}
</MediaQuery>

<style lang="scss">
	.language-picker {
		position: relative;
		display: inline-block;
		user-select: none;
		font-family: 'Roundo';
		text-transform: uppercase;
		width: 120px;

		.selected-language {
			display: flex;
			align-items: center;
			font-size: 1.5em;
			cursor: pointer;
			color: var(--black);
			mix-blend-mode: difference; /* Inverts colors based on background */
			// filter: drop-shadow(0 0 2px rgba(0, 0, 0, 1));

			.language {
				margin: 0 8px;
			}
		}

		.dropdown {
			position: absolute;
			top: 100%;
			left: 0;
			border-radius: 5px;
			width: 100%;
			z-index: 10;
			margin-top: 5px;

			.dropdown-item {
				padding: 10px;
				font-family: 'Roundo';
				font-size: 1.25em;
				cursor: pointer;
				transition: background 0.3s;
				color: var(--black);
				// filter: drop-shadow(0 0 2px rgba(0, 0, 0, 1));

				&:hover {
					color: var(--blue-600);
				}
			}
		}
	}
	.mobile-language-picker {
		margin: 0;
		position: relative;
		display: inline-block;
		user-select: none;
		font-family: 'Roundo';
		text-transform: uppercase;
		color: var(--black);

		.selected-language {
			display: flex;
			align-items: center;
			font-size: 1.5em;
			cursor: pointer;
			.language {
				margin: 0 8px;
			}
		}

		.dropdown {
			position: absolute;
			top: 100%;
			left: 0;
			border-radius: 5px;
			width: 100%;
			z-index: 10;
			margin-top: 5px;

			.dropdown-item {
				padding: 10px;
				margin-left: 25px;
				font-family: 'Roundo';
				font-size: 1.25em;
				cursor: pointer;
				transition: background 0.3s;
			}
		}
	}
</style>
