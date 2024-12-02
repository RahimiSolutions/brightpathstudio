<script lang="ts">
	import MediaQuery from '../MediaQuery.svelte';
	import LogoNavbar from '$lib/images/logo-nostudio.png';
	import { slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import { language, locale, t } from '$lib/text/i18n';
	import LanguagePicker from '../LanguagePicker.svelte';

	let closed = true;
	let isMenuOpen = false; // This will be used for binding the checkbox state.
	let isLanguagePickerOpen = false;
	let height = '70px';

	function handleMobileMenuClick() {
		if (isMenuOpen) {
			height = '98%';
			closed = false;
		} else {
			height = '70px';
			closed = true;
		}
	}

	function handleMenuChoice() {
		if (!closed) {
			isMenuOpen = false; // This will uncheck the checkbox.
			height = '70px';
			closed = true;
		}
	}

	function toggleLanguage() {
		$language = $language === 'en' ? 'no' : 'en';
		setTimeout(() => {
			$locale = $locale === 'en' ? 'no' : 'en';
			saveLanguageToLocalStorage($locale);
		}, 300);
	}
	function saveLanguageToLocalStorage(language: string) {
		localStorage.setItem('languagePreferance', language);
	}
</script>

<MediaQuery query="(max-width: 999px)" let:matches>
	{#if matches}
		{#key $locale}
			<div
				class="mobile-nav"
				style:height
				transition:slide={{ delay: 100, duration: 300, easing: quintOut, axis: 'y' }}
			>
				<div class="mobile-nav-closed">
					<div class="mobile-nav-logo">
						<a href="/"><img src={LogoNavbar} alt="BrighPath" /></a>
					</div>
					<div class="mobile-nav-dropdown">
						<!-- svelte-ignore a11y-no-static-element-interactions svelte-ignore a11y-click-events-have-key-events -->
						<label class="burger" for="burger">
							<input
								type="checkbox"
								id="burger"
								bind:checked={isMenuOpen}
								on:change={handleMobileMenuClick}
							/>
							<span></span>
							<span></span>
							<span></span>
						</label>
					</div>
				</div>
				{#if !closed}
					<div class="mobile-nav-sidebar-content">
						<p>
							<a href="https://www.brightpath.studio" on:click={handleMenuChoice}
								>{@html $t('home')}</a
							>
						</p>
						<p>
							<a href="https://www.brightpath.studio/#about" on:click={handleMenuChoice}
								>{@html $t('about')}</a
							>
						</p>
						<p>
							<a href="https://booking.brightpath.studio/" on:click={handleMenuChoice}
								>{@html $t('contact')}</a
							>
						</p>
						<div class="language-picker">
							<LanguagePicker />
						</div>

						<!-- <div class="contact-card">
							<div class="card-title">{@html $t('contact')}</div>
							<div class="box">
								<div class="title">{@html $t('email')}</div>
								<div class="content">
									<a href="mailto:contact@rahimisolutions.com">contact@rahimisolutions.com</a>
								</div>
							</div>
							<div class="box">
								<div class="title">Instagram</div>
								<div class="content">
									<a href="https://ig.me/m/rahimisolutions">@rahimisolutions</a>
								</div>
							</div>
						</div> -->
					</div>
				{/if}
			</div>
		{/key}
	{/if}
</MediaQuery>

<style lang="scss">
	.mobile-nav {
		z-index: 100;
		width: 97%;
		position: fixed;
		top: 1%;
		bottom: 1%;
		left: 1.5%;
		right: 1.5%;
		background-color: rgba(120, 174, 255, 0.15);
		border: 0.5px solid var(--blue-600);
		backdrop-filter: blur(8px);
		border-radius: 15px;
		box-shadow: 5px 5px 12px 0 rgb(0, 0, 0, 0.1);
		transition: 0.4s ease;
		.mobile-nav-closed {
			height: 70px;
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			.mobile-nav-dropdown {
				margin: 0 1em 0 0;
				height: 100%;
				display: flex;
				justify-content: center;
				align-items: center;
			}
			.mobile-nav-logo {
				a {
					height: 30px;
					display: flex;
					align-items: center;
					margin: 0 0 0 1em;
					text-decoration: none;
					img {
						max-height: 100%;
					}
				}
			}
		}
	}

	.mobile-nav-sidebar-content {
		height: 100%;
		display: flex;
		flex-direction: column;
		align-items: start;

		box-shadow: 5px 15px 12px 0 rgb(0, 0, 0, 0.1);
		p {
			padding-left: 10%;
			margin: 1em 0 1em 0;
			a {
				font-family: 'Roundo';
				text-transform: uppercase;
				text-decoration: none;
				color: var(--black);
				font-size: 1.5em;
			}
		}
		.language-picker {
			padding-left: 10%;
			margin: 1em 0 1em 0;
		}
	}

	.burger {
		position: relative;
		width: 30px;
		height: 20px;
		background: transparent;
		cursor: pointer;
		display: block;
	}

	.burger input {
		display: none;
	}

	.burger span {
		display: block;
		position: absolute;
		height: 3px;
		width: 100%;
		background: var(--grey);
		border-radius: 9px;
		opacity: 1;
		left: 0;
		transform: rotate(0deg);
		transition: 0.25s ease-in-out;
	}

	.burger span:nth-of-type(1) {
		top: 0px;
		transform-origin: left center;
	}

	.burger span:nth-of-type(2) {
		top: 50%;
		transform: translateY(-50%);
		transform-origin: left center;
	}

	.burger span:nth-of-type(3) {
		top: 100%;
		transform-origin: left center;
		transform: translateY(-100%);
	}

	.burger input:checked ~ span:nth-of-type(1) {
		transform: rotate(45deg);
		top: -1px;
		left: 4px;
	}

	.burger input:checked ~ span:nth-of-type(2) {
		width: 0%;
		opacity: 0;
	}

	.burger input:checked ~ span:nth-of-type(3) {
		transform: rotate(-45deg);
		top: 20px;
		left: 3px;
	}
</style>
