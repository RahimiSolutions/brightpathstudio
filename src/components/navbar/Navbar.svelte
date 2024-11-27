<script>
	import logo from '$lib/images/logo-nobg-nopad.png';
	import { t } from '$lib/text/i18n';
	import LanguagePicker from '../LanguagePicker.svelte';
	import MediaQuery from '../MediaQuery.svelte';
</script>

<MediaQuery query="(min-width: 1000px)" let:matches>
	{#if matches}
		<nav>
			<div class="container">
				<div class="left">
					<img src={logo} alt="brightpath studio" />
				</div>
				<div class="right">
					<a href="/">{@html $t('home')}</a>
					<a href="https://checkout.brightpath.studio/">{@html $t('about')}</a>
					<a href="https://booking.brightpath.studio/">{@html $t('contact')}</a>
				</div>
			</div>
			<div class="language-picker">
				<LanguagePicker />
			</div>
		</nav>
	{/if}
</MediaQuery>

<style lang="scss">
	::selection {
		background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
		color: #000; /* Black text for contrast */
		text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
	}
	nav {
		position: fixed;
		left: 50%;
		top: 25px;
		transform: translateX(-50%);
		z-index: 99;
		width: 60%;
		border-radius: 25px;
		background-color: rgba(120, 174, 255, 0.15);
		border: 0.5px solid var(--blue-600);
		backdrop-filter: blur(8px);
		height: 90px;
		.container {
			height: 100%;
			max-width: 100%;
			display: flex;
			justify-content: space-between;

			.left {
				padding-left: 60px;
				width: 50%;
				height: 100%;
				display: flex;
				justify-content: start;
				align-items: center;
				img {
					width: clamp(150px, 60%, 400px);
				}
			}
			.right {
				overflow: hidden;
				display: flex;
				width: 100%;
				padding-right: 60px;
				justify-content: end;
				gap: 25px;
				align-items: center;
				a {
					font-family: 'Roundo';
					font-size: clamp(1.25rem, 0.4348rem + 1.3043vw, 2rem);
					font-weight: 5 00;
					color: var(--black);
					text-decoration: none;
					text-transform: capitalize;
					transition: 0.3s ease-out;
					cursor: pointer;
					&:hover {
						color: var(--blue-600);
					}
				}
			}
		}
		.language-picker {
			position: absolute;
			right: -125px;
			top: 20px;
		}
	}
</style>
