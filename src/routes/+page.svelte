<script lang="ts">
	import MediaQuery from '../components/MediaQuery.svelte';
	import bgTexture from '$lib/images/bg-texture.png';
	import reviwerOne from '$lib/images/reviewerOne.png';
	import reviwerTwo from '$lib/images/reviewerTwo.png';
	import reviwerThree from '$lib/images/reviewerThree.png';
	import { locale, t } from '$lib/text/i18n';
	import { quintOut } from 'svelte/easing';
	import { fade, slide } from 'svelte/transition';
	import BlueArrow from '$lib/images/blue-arrow.svelte';
	import Button from '../components/UiElements/button.svelte';
	import ReviewBubble from '../components/UiElements/ReviewBubble.svelte';
	import { onMount } from 'svelte';
	const reviews = [
		{ imageSrc: reviwerOne, reviewKey: 'reviewOne' },
		{ imageSrc: reviwerTwo, reviewKey: 'reviewTwo' },
		{ imageSrc: reviwerThree, reviewKey: 'reviewThree' }
		// Add more reviews as needed
	];

	// Define multiple sets of positions
	const positionSets = [
		[
			{ top: '5%', left: '5%' },
			{ top: '15%', right: '10%' },
			{ bottom: '0%', left: '10%' }
		],
		[
			{ top: '5%', right: '10%' },
			{ top: '5%', left: '0%' },
			{ bottom: '5%', right: '20%' }
		]
		// Add more sets as needed
	];

	let selectedPositions:
		| (
				| { top: string; left: string; right?: undefined; bottom?: undefined }
				| { top: string; right: string; left?: undefined; bottom?: undefined }
				| { bottom: string; left: string; top?: undefined; right?: undefined }
		  )[]
		| (ArrayLike<unknown> | { [s: string]: unknown })[];

	onMount(() => {
		// Randomly select a set of positions
		selectedPositions = positionSets[Math.floor(Math.random() * positionSets.length)];
	});
</script>

<MediaQuery query="(min-width: 1000px)" let:matches>
	{#if matches}
		<div class="wrapper" transition:fade={{ delay: 0, duration: 500 }}>
			{#key $locale}
				<div transition:slide={{ delay: 100, duration: 1000, easing: quintOut, axis: 'y' }}>
					<div class="container">
						<img class="bg-texture" src={bgTexture} alt="Background texture" />
						<section class="hero-section">
							<div class="top">
								{@html $t('headline')}
								<div class="blue-arrow">
									<BlueArrow width="12vw" />
								</div>
							</div>

							{#if selectedPositions}
								{#each reviews as review, i}
									{#if selectedPositions[i]}
										<div
											class="review-bubble-wrapper"
											style="position: absolute; {Object.entries(selectedPositions[i])
												.map(([key, value]) => `${key}: ${value};`)
												.join(' ')}"
										>
											<ReviewBubble imageSrc={review.imageSrc} review={$t(review.reviewKey)} />
										</div>
									{/if}
								{/each}
							{/if}

							<div class="bottom">
								{@html $t('sub-headline')}
							</div>
							<div class="cta">
								<div class="button">
									<Button link="https://booking.brightpath.studio/" />
								</div>
							</div>
						</section>
						<section class="dashboard-gif">
							<video src="/videos/dashboard.mp4" autoplay loop muted playsinline class="video"
							></video>
						</section>
						<section class="process-section"></section>
					</div>
				</div>
			{/key}
		</div>
	{/if}
</MediaQuery>

<MediaQuery query="(max-width: 999px)" let:matches>
	{#if matches}
		<div class="wrapper" transition:fade={{ delay: 0, duration: 500 }}>
			{#key $locale}
				<div transition:slide={{ delay: 100, duration: 1000, easing: quintOut, axis: 'y' }}>
					<div class="mobile-container">
						<section class="hero-section">
							<div class="top">
								{@html $t('headline')}
							</div>
							<div class="bottom">{@html $t('sub-headline-mobile')}</div>

							<div class="cta">
								<div class="button">
									<Button link="https://booking.brightpath.studio/" />
								</div>
							</div>
						</section>
						<section class="dashboard-gif">
							<video src="/videos/dashboard.mp4" autoplay loop muted playsinline class="video"
							></video>
						</section>
						<section class="process-section"></section>
					</div>
				</div>
			{/key}
		</div>
	{/if}
</MediaQuery>

<style lang="scss">
	::selection {
		background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
		color: #000; /* Black text for contrast */
		text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
	}
	.container {
		font-family: 'Roundo';
		color: var(--black);
		.bg-texture {
			z-index: 0;
			position: absolute;
			top: 20px;
			left: 50%;
			transform: translateX(-50%);
		}
		.hero-section {
			position: relative;
			z-index: 2;
			width: 80%;
			margin: 50px auto;

			.top {
				width: 60%;
				margin: auto;
				font-size: var(--fs-800);
				font-weight: 600;
				text-transform: capitalize;
				text-align: center;
				position: relative;
				.blue-arrow {
					position: absolute;
					right: 20%;
					top: 120%;
					transform: scaleX(-1) rotate(20deg);
				}
			}
			.bottom {
				width: 60%;
				margin: 100px auto;
				color: var(--blue-600);
				font-size: var(--fs-500);
				font-weight: 600;
				letter-spacing: 1px;
				text-transform: capitalize;
				text-align: start;
			}
			.cta {
				display: flex;
				justify-content: center;
				.button {
				}
			}
		}
		.dashboard-gif {
			position: relative;
			display: flex;
			justify-content: center;
			width: 80%;
			margin: 50px auto;

			video {
				max-width: 100%;
				border-radius: 25px;
				box-shadow: 8px 12px 0 0 rgba(0, 0, 0, 0.6);
			}
		}
	}
	.mobile-container {
		.hero-section {
			width: 90%;
			margin: 120px auto 100px auto;
			border-radius: 100vw;
			background-image: radial-gradient(#dbdbdb 0.9px, #fdfdfd 0.9px);
			background-size: 25px 25px;

			font-family: 'Roundo';

			.top {
				width: 100%;
				margin: auto;
				font-size: var(--fs-600);
				font-weight: 600;
				text-transform: capitalize;
				text-align: center;
				position: relative;
				.blue-arrow {
					position: absolute;
					right: 20%;
					top: 120%;
					transform: scaleX(-1) rotate(20deg);
				}
			}
			.bottom {
				width: 90%;
				margin: 50px 0;
				color: var(--blue-600);
				font-size: var(--fs-400);
				font-weight: 600;
				letter-spacing: 1px;
				text-transform: capitalize;
				text-align: start;
			}
			.cta {
				display: flex;
				justify-content: center;
				.button {
				}
			}
		}
		.dashboard-gif {
			width: 90%;
			margin: auto;
			video {
				max-width: 100%;
				border-radius: 10px;
				box-shadow: 4px 6px 0 0 rgba(0, 0, 0, 0.6);
			}
		}
	}
</style>
