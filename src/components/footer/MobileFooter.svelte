<script>
	import logoFooter from '$lib/images/logo-nostudio.png';
	import MediaQuery from '../MediaQuery.svelte';
	import { t } from '$lib/text/i18n';
	import Envelope from '$lib/icons/envelope.svelte';
	import Phone from '$lib/icons/phone.svelte';
	import Location from '$lib/icons/location.svelte';
	import Facebook from '$lib/icons/facebook.svelte';
	import Instagram from '$lib/icons/instagram.svelte';
</script>

<MediaQuery query="(max-width: 999px)" let:matches>
	{#if matches}
		<footer>
			<div class="title"><h1>{@html $t('contact-us')}</h1></div>
			<div class="container">
				<div class="contact-container">
					<div class="content">
						<div class="right">
							<ul>
								<li>
									<Envelope />
									<p>contact@brightpath.com</p>
								</li>
								<li>
									<Phone />
									<p>+47 699 79 689</p>
								</li>
								<li>
									<Location />
									<p>Oslo, Norway</p>
								</li>
							</ul>
						</div>
					</div>
				</div>
				<div class="social-container">
					<div class="right">
						<ul>
							<li>
								<a href="https://www.facebook.com/"
									><Facebook fill="#fff" />
									<p>Facebook</p></a
								>
							</li>
							<li>
								<a href="https://www.instagram.com/"
									><Instagram fill="#fff" />
									<p>Instagram</p></a
								>
							</li>
						</ul>
					</div>
				</div>
			</div>
			<img class="logo-footer" src={logoFooter} alt="" />

			<div class="legal">
				<p>{@html $t('copyright')}</p>
				<ul>
					<li>{@html $t('terms-conditions')}</li>
					<li>{@html $t('privacy-policy')}</li>
				</ul>
			</div>
		</footer>
	{/if}
</MediaQuery>

<style lang="scss">
	footer {
		::selection {
			background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
			color: #fff; /* Black text for contrast */
			text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
		}
		width: 100%;
		margin: 300px auto 0 auto;
		position: relative;
		border-radius: 50px 50px 0 0;
		background: radial-gradient(
			circle at 50% 150%,
			hsl(216, 60%, 50%) 25%,
			rgba(253, 253, 253, 1) 115%
		);
		box-shadow: 0px -4px 0px 0 rgba(0, 0, 0, 0.25);
		font-family: 'Roundo';
		color: var(--blue-800);
		.title {
			padding: 25px 15px 0 15px;
			width: 100%;
			h1 {
				font-size: var(--mfs-600);
				text-align: center;
				font-weight: 500;
			}
		}

		.container {
			padding: 25px 15px 0 15px;
			display: flex;
			margin-bottom: 24px;

			.social-container {
				flex: 1;
				display: flex;
				flex-direction: column;
				justify-content: start;
				.right {
					width: 100%;
					ul {
						flex-direction: column;
						align-items: center;
						display: flex;
						li {
							list-style-type: none;
							font-weight: 500;
							font-size: var(--mfs-400);
							margin-bottom: 16px;
							
							a{
								display: flex;
								align-items: center;
								gap: 8px;
								text-decoration: none;
								color: var(--blue-800);
							}
						}
					}
				}
			}
			.contact-container {
				position: relative;
				flex: 1;
				.content {
					display: flex;
					flex-direction: column;
					justify-content: start;
					.right {
						ul {
							li {
								list-style-type: none;
								font-size: var(--mfs-400);
								font-weight: 500;
								margin-bottom: 16px;
								display: flex;
								gap: 8px;
								align-items: center;
							}
						}
					}
				}
			}
		}

		.logo-footer {
			width: fit-content;
			width: 100%;
			mix-blend-mode: screen;
		}
		.legal {
			width: 100%;
			text-align: center;
			display: flex;
			flex-direction: column;
			justify-content: center;
			gap: 2px;
			color: rgb(9, 22, 66);
			p {
				font-size: var(--mfs-350);
				font-weight: 500;
			}
			ul {
				display: flex;
				justify-content: space-evenly;
				gap: 4px;
				li {
					list-style-type: none;
					font-size: var(--mfs-350);
					font-weight: 500;
				}
			}
		}

		// height: 50vh;
		// background-image: radial-gradient(var(--blue-300) 20px, var(--white) 10px);
		// background-size: 5vw 5vw;
	}
</style>
