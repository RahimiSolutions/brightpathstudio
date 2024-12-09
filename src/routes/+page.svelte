<script lang="ts">
	import MediaQuery from '../components/MediaQuery.svelte';

	import funnelPieceOne from '$lib/images/Funnel_piece_one.svg';
	import funnelPieceTwo from '$lib/images/Funnel_piece_two.svg';
	import funnelPieceThree from '$lib/images/Funnel_piece_three.svg';
	import funnelPieceFour from '$lib/images/Funnel_piece_four.svg';
	import funnelPieceFive from '$lib/images/Funnel_piece_five.svg';
	import character from '$lib/images/Character.svg';
	import characterAds from '$lib/images/Character-googleads.svg';
	import bgWaves from '$lib/images/waves.svg';
	import landingpage from '$lib/images/landingpage.png';
	import booking from '$lib/images/booking.png';
	import bend from '$lib/images/bend.svg';

	import characterFunnel from '$lib/images/character-funnel.png';

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
	import { onDestroy, onMount } from 'svelte';
	import ReviewCarousel from '../components/UiElements/ReviewCarousel.svelte';
	import StepCard from '../components/UiElements/StepCard.svelte';
	import Faq from '../components/UiElements/Faq.svelte';
	import ComparisonCards from '../components/UiElements/ComparisonCards.svelte';
	import Toggle from '../components/UiElements/toggle.svelte';
	import Lenis from 'lenis';
	import 'lenis/dist/lenis.css';
	import MobileReviewCarousel from '../components/UiElements/MobileReviewCarousel.svelte';
	import gsap from 'gsap';

	// const animateOnClick = {e} => {
	// 	const {target} = e;

	// 	gsap.to(target, {x: += 100})
	// }

	let annualPrice = false;
	let lenis: Lenis;
	let activeIndex: number | null = 0;

	function toggle(index: number) {
		activeIndex = activeIndex === index ? null : index;
	}
	const funnellevels = [
		{ title: 'funnel-one-title', text: 'funnel-one-text' },
		{ title: 'funnel-two-title', text: 'funnel-two-text' },
		{ title: 'funnel-three-title', text: 'funnel-three-text' },
		{ title: 'funnel-four-title', text: 'funnel-four-text' }
	];

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

	function getSavings(annualPrice: boolean) {
		switch (annualPrice) {
			case false:
				return $t('monthly-saving');
			case true:
				return $t('annual-saving');
			default:
				return null;
		}
	}
	onMount(() => {
		// Randomly select a set of positions
		selectedPositions = positionSets[Math.floor(Math.random() * positionSets.length)];

		lenis = new Lenis({
			duration: 1.3,
			easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
			touchMultiplier: 2,
			infinite: false
		});

		function raf(time: any) {
			lenis.raf(time);
			requestAnimationFrame(raf);
		}

		requestAnimationFrame(raf);
	});

	onDestroy(() => {
		if (lenis) {
			lenis.destroy();
		}
	});
</script>

<svelte:head>
	<script src="https://unpkg.com/lenis@1.1.17/dist/lenis.min.js"></script>
</svelte:head>

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
						<section class="process-section">
							<h1 class="process-title">{@html $t('process-title')}</h1>
							<p class="process-subtitle">{@html $t('process-subtitle')}</p>
						</section>
						<section class="funnel-section">
							<div class="back">
								<ul>
									<li>
										<h1>{@html $t('leads-count')}</h1>
										<p>{@html $t('leads-generated')}</p>
									</li>
									<li>
										<h1>{@html $t('customer-count')}</h1>
										<p>{@html $t('happy-customers')}</p>
									</li>
									<li>
										<h1>{@html $t('projects-count')}</h1>
										<p>{@html $t('successful-projects')}</p>
									</li>
								</ul>
							</div>

							<div class="front">
								<div class="funnel">
									<div class="level">
										<div class="funnel-piece one">
											<img src={funnelPieceOne} alt="Funnel piece one" />
											<div class="text">
												{@html $t('funnel-one')}
											</div>
										</div>
									</div>
									<div class="level">
										<div class="funnel-piece two">
											<img src={funnelPieceTwo} alt="Funnel piece two" />
											<div class="text">
												{@html $t('funnel-two')}
											</div>
										</div>
									</div>
									<div class="level">
										<div class="funnel-piece three">
											<img src={funnelPieceThree} alt="Funnel piece three" />
											<div class="text">
												{@html $t('funnel-three')}
											</div>
										</div>
									</div>
									<div class="level">
										<div class="funnel-piece four">
											<img src={funnelPieceFour} alt="Funnel piece four" />
											<div class="text">
												{@html $t('funnel-four')}
											</div>
										</div>
									</div>
									<div class="level">
										<div class="funnel-piece five">
											<img src={funnelPieceFive} alt="Funnel piece five" />
											<div class="text"></div>
										</div>

										<img
											class="character"
											src={character}
											alt="animated character pointing at funnel"
										/>
									</div>
								</div>
								<div class="funnel-dropdown-container">
									{#each funnellevels as { title, text }, index}
										<div class="funnel-item" class:active={activeIndex === index}>
											<button
												class="funnel-title"
												on:click={() => toggle(index)}
												aria-expanded={activeIndex === index}
											>
												<span class="funnel-title-text">{@html $t(title)}</span>
												<span class="icon">{activeIndex === index ? '−' : '+'}</span>
											</button>

											{#if activeIndex === index}
												<div class="funnel-text" transition:slide={{ duration: 300 }}>
													{@html $t(text)}
												</div>
											{/if}
										</div>
									{/each}
								</div>
							</div>
						</section>
						<section class="review-section" id="reviews">
							<ReviewCarousel />
						</section>

						<section class="function-ads">
							<div class="content">
								<div class="text-container">
									<div class="tag">{@html $t('function-ads-tag')}</div>
									<div class="title">{@html $t('function-ads-title')}</div>
									<div class="text">{@html $t('function-ads-text')}</div>
									<Button link="https://booking.brightpath.studio/" />
								</div>
								<div class="image">
									<img src={characterAds} alt="Character holding google ads logo" />
								</div>
							</div>
						</section>
						<section class="function-landingpage">
							<div class="content">
								<div class="image">
									<img src={landingpage} alt="Mockups of landingpages" />
								</div>
								<div class="text-container">
									<div class="tag">{@html $t('function-landing-tag')}</div>
									<div class="title">{@html $t('function-landing-title')}</div>
									<div class="text">{@html $t('function-landing-text')}</div>
									<Button link="https://booking.brightpath.studio/" />
								</div>
							</div>
						</section>
						<section class="function-booking">
							<div class="bend">
								<img src={bend} alt="background illustration" />
							</div>
							<div class="content">
								<div class="text-container">
									<div class="tag">{@html $t('function-booking-tag')}</div>
									<div class="title">{@html $t('function-booking-title')}</div>
									<div class="text">{@html $t('function-booking-text')}</div>
									<Button link="https://booking.brightpath.studio/" />
								</div>
								<div class="image">
									<img src={booking} alt="Device mockups for booking page" />
								</div>
							</div>
						</section>

						<section class="comparison-section">
							<h1>{@html $t('features-title')}</h1>
							<ComparisonCards />
							<div class="savings-section">
								<div class="toggle">
									<p>{@html $t('monthly')}</p>
									<Toggle bind:annualPrice />
									<p>{@html $t('annual')}</p>
								</div>
								<div class="saving-amount">
									<p>
										{@html $t('save')}

										<span class="highlight-blue">{getSavings(annualPrice)}</span>

										{@html $t('with-brightpath')}
									</p>
								</div>
							</div>
							<Button link="https://booking.brightpath.studio/" />
						</section>

						<section class="function-ads">
							<div class="content">
								<div class="text-container">
									<div class="tag">{@html $t('function-invoice-tag')}</div>
									<div class="title">{@html $t('function-invoice-title')}</div>
									<div class="text">{@html $t('function-invoice-text')}</div>
									<Button link="https://booking.brightpath.studio/" />
								</div>
								<div class="image"></div>
							</div>
						</section>

						<section class="steps-section" id="about">
							<div class="text">
								<div class="title">{@html $t('steps-title')}</div>
								<div class="subtitle">{@html $t('steps-subtitle')}</div>
							</div>
							<div class="steps">
								<StepCard number="1" title={$t('step-one-title')} text={$t('step-one-text')} />
								<StepCard number="2" title={$t('step-two-title')} text={$t('step-two-text')} />
								<StepCard number="3" title={$t('step-three-title')} text={$t('step-three-text')} />
							</div>
							<div class="cta">
								<Button link="https://booking.brightpath.studio/" />
							</div>
						</section>

						<section class="faq-section">
							<div class="title">{@html $t('faq-title')}</div>
							<Faq />
						</section>

						<section class="ready-section">
							<div class="back">
								<img src={bgWaves} alt="Abstract illustration" />
							</div>
							<div class="front">
								<div class="container">
									<div class="title">{@html $t('cta-title')}</div>
									<div class="text">
										<p>
											{@html $t('cta-text')}
										</p>
									</div>
									<div class="button">
										<Button link="https://booking.brightpath.studio/" />
									</div>
								</div>
							</div>
						</section>
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
								<h1>{@html $t('headline')}</h1>
							</div>
							<div class="bottom">
								<p>{@html $t('sub-headline-mobile')}</p>
								<div class="reviewers">
									<ReviewBubble
										imageSrc={reviews.at(0)?.imageSrc}
										review={$t(reviews.at(0)?.reviewKey)}
									/>
									<ReviewBubble
										imageSrc={reviews.at(1)?.imageSrc}
										review={$t(reviews.at(1)?.reviewKey)}
									/>
									<ReviewBubble
										imageSrc={reviews.at(2)?.imageSrc}
										review={$t(reviews.at(2)?.reviewKey)}
									/>
								</div>
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
						<section class="process-section">
							<div class="title"><h1>{@html $t('process-title')}</h1></div>
							<div class="text"><p>{@html $t('process-subtitle-mobile')}</p></div>
							<div class="illustration"><img src={characterFunnel} alt="" /></div>
						</section>
						<section class="review-section">
							<div class="stats">
								<ul>
									<li>
										<h1>{@html $t('leads-count')}</h1>
										<p>{@html $t('leads-generated')}</p>
									</li>
									<li>
										<h1>{@html $t('customer-count')}</h1>
										<p>{@html $t('happy-customers')}</p>
									</li>
									<li>
										<h1>{@html $t('projects-count')}</h1>
										<p>{@html $t('successful-projects')}</p>
									</li>
								</ul>
							</div>
							<div class="review-carousel" id="reviews">
								<MobileReviewCarousel />
							</div>
						</section>

						<section class="function-ads">
							<div class="container">
								<div class="title">
									<div class="tag">{@html $t('function-ads-tag')}</div>
									<div class="title">{@html $t('function-ads-title')}</div>
								</div>
								<div class="content">
									<div class="text">{@html $t('function-ads-text')}</div>
									<img src={characterAds} alt="Character holding google ads logo" />
								</div>
							</div>
							<Button link="https://booking.brightpath.studio/" />
						</section>
						<section class="function-landingpage">
							<div class="content">
								<div class="text-container">
									<div class="tag">{@html $t('function-landing-tag')}</div>
									<div class="title">{@html $t('function-landing-title')}</div>
									<div class="text">{@html $t('function-landing-text')}</div>
								</div>
								<div class="image">
									<img src={landingpage} alt="Mockups of landingpages" />
								</div>
							</div>
							<Button link="https://booking.brightpath.studio/" />
						</section>
						<section class="function-booking">
							<div class="bend">
								<img src={bend} alt="background illustration" />
							</div>
							<div class="content">
								<div class="text-container">
									<div class="tag">{@html $t('function-booking-tag')}</div>
									<div class="title">{@html $t('function-booking-title')}</div>
									<div class="text">{@html $t('function-booking-text')}</div>
								</div>
								<div class="image">
									<img src={booking} alt="Device mockups for booking page" />
								</div>
							</div>
							<Button link="https://booking.brightpath.studio/" />
						</section>

						<section class="comparison-section">
							<h1>{@html $t('features-title')}</h1>
							<ComparisonCards />
							<div class="savings-section">
								<div class="toggle">
									<p>{@html $t('monthly')}</p>
									<Toggle bind:annualPrice />
									<p>{@html $t('annual')}</p>
								</div>
								<div class="saving-amount">
									<p>
										{@html $t('save')}

										<span class="highlight-blue">{getSavings(annualPrice)}</span>

										{@html $t('with-brightpath')}
									</p>
								</div>
							</div>
							<Button link="https://booking.brightpath.studio/" />
						</section>

						<section class="function-ads">
							<div class="container">
								<div class="title">
									<div class="tag">{@html $t('function-invoice-tag')}</div>
									<div class="title">{@html $t('function-invoice-title')}</div>
								</div>
								<div class="content">
									<div class="text">{@html $t('function-invoice-text')}</div>
									<div class="image"></div>
								</div>
							</div>
							<Button link="https://booking.brightpath.studio/" />
						</section>

						<section class="steps-section" id="about">
							<div class="text">
								<div class="title">{@html $t('steps-title')}</div>
								<div class="subtitle">{@html $t('steps-subtitle')}</div>
							</div>
							<div class="steps">
								<StepCard number="1" title={$t('step-one-title')} text={$t('step-one-text')} />
								<StepCard number="2" title={$t('step-two-title')} text={$t('step-two-text')} />
								<StepCard number="3" title={$t('step-three-title')} text={$t('step-three-text')} />
							</div>
							<div class="cta">
								<Button link="https://booking.brightpath.studio/" />
							</div>
						</section>

						<section class="faq-section">
							<div class="title">{@html $t('faq-title')}</div>
							<Faq />
						</section>

						<section class="ready-section">
							<div class="back">
								<img src={bgWaves} alt="Abstract illustration" />
							</div>
							<div class="front">
								<div class="container">
									<div class="title">{@html $t('cta-title')}</div>
									<div class="text">
										<p>
											{@html $t('cta-text')}
										</p>
									</div>
									<div class="button">
										<Button link="https://booking.brightpath.studio/" />
									</div>
								</div>
							</div>
						</section>
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
		overflow-x: clip;
		position: relative;
		:global(.highlight-blue) {
			color: var(--blue-600);
			font-weight: 600;
			&::selection {
				background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
				color: #000; /* Black text for contrast */
				text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
			}
		}
		:global(.highlight-red) {
			color: #9c0000;
			font-weight: 600;
			&::selection {
				background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
				color: #000; /* Black text for contrast */
				text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
			}
		}
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
			margin: 170px auto;

			.top {
				width: 60%;
				margin: auto;
				font-size: var(--fs-700);
				font-weight: 500;
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
				font-size: var(--fs-400);
				font-weight: 500;
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

		.process-section {
			width: 80%;
			margin: 100px auto 150px auto;
			.process-title {
				text-align: center;
				font-size: var(--fs-800);
				font-variation-settings: 'wght' 600;
				text-transform: capitalize;
				margin: 20px 0;
			}
			.process-subtitle {
				font-size: var(--fs-500);
				width: 60ch;
				margin: auto;
				text-align: center;
			}
		}

		.funnel-section {
			margin: 10vh 0;
			position: relative;
			display: flex;
			align-items: center;
			.back {
				position: absolute;
				z-index: 0;
				width: 50%;
				background-color: rgba(120, 174, 255, 0.15);
				color: #5c6066;
				font-family: 'Sfpro';
				ul {
					li {
						border-bottom: 2px solid var(--white);
						padding: 5% 5%;
						h1 {
							font-size: var(--fs-800);
						}
						p {
							font-size: var(--fs-600);
						}
					}
				}
			}
			.front {
				position: relative;
				z-index: 1;
				width: 100%;
				display: flex;
				justify-content: center;
				.funnel {
					width: 600px;
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					position: relative;
					.funnel-piece {
						position: relative;
						.text {
							text-align: center;
							position: absolute;
							top: 50%;
							left: 50%;
							transform: translate(-50%, -35%);
							color: var(--white);
							width: 80%;
						}
					}

					.one {
						font-size: clamp(1.5rem, 0.9565rem + 0.8696vw, 2rem);
						.text {
							transform: translate(-50%);
						}
					}
					.two {
						font-size: clamp(1rem, 0.5652rem + 0.6957vw, 1.4rem);
						.text {
							width: 70%;
						}
					}
					.three {
						font-size: clamp(1rem, 0.7283rem + 0.4348vw, 1.25rem);
						.text {
							width: 70%;
						}
					}
					.four {
						font-size: clamp(0.75rem, 0.4783rem + 0.4348vw, 1rem);
					}
					.five {
						font-size: clamp(0.75rem, 0.4783rem + 0.4348vw, 1rem);
					}

					.character {
						bottom: 0;
						left: -15%;
						transform: translateX(50%);
						position: absolute;
					}
				}
				.funnel-dropdown-container {
					position: absolute;
					left: 75%;
					width: 30ch;
					font-family: 'Roundo';
					.funnel-item {
						background-color: rgba(255, 255, 255, 0.05);
						border-radius: 8px;
						margin-bottom: 1rem;
						transition: all 0.3s ease;

						&:hover {
							background-color: rgba(0, 0, 0, 0.05);
						}

						&.active {
							background-color: #ffffff;
							box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
							.funnel-title {
								color: var(--blue-700, #124fa9);
							}
						}
						.funnel-title {
							background: none;
							border: none;
							cursor: pointer;
							display: flex;
							justify-content: space-between;
							align-items: center;
							width: 100%;
							padding: 1.25rem;
							font-family: inherit;
							font-size: var(--fs-600);
							font-weight: 500;
							color: var(--blue-700);
							transition: color 0.3s ease;
							.funnel-title-text {
								text-align: left;
								flex-grow: 1;
								padding-right: 1rem;
							}
							.icon {
								font-size: 1.5rem;
								min-width: 24px;
								display: flex;
								justify-content: center;
								align-items: center;
							}
						}
						.funnel-text {
							padding: 0 1rem 1rem;
							font-family: 'Sfpro', sans-serif;
							font-size: var(--fs-400);
							line-height: 1.6;
							color: var(--blue-700, #124fa9);
						}
					}
				}
			}
		}
		.review-section {
			scroll-margin-top: 150px;
			margin: 250px 0 150px 0;
		}

		.function-ads {
			margin: 100px 0;
			.content {
				width: 80%;
				margin: auto;
				display: flex;
				.text-container {
					flex: 1;

					:global(.highlight-blue) {
						color: var(--blue-500);
						font-weight: 500;
					}
					.tag {
						font-size: var(--fs-400);
						color: var(--grey);
					}
					.title {
						font-size: var(--fs-700);
					}
					.text {
						font-size: var(--fs-400);
						width: 40ch;
						font-weight: 500;
						margin: 24px 0;
					}
				}
				.image {
					display: flex;
					flex: 1;
					justify-content: center;
					img {
					}
				}
			}
		}

		.function-landingpage {
			margin: 100px 0;
			position: relative;
			z-index: 5;
			.content {
				width: 90%;
				margin: auto;
				display: flex;
				gap: 2rem;
				.text-container {
					flex: 1;

					:global(.highlight-blue) {
						color: var(--blue-500);
						font-weight: 500;
					}
					.tag {
						font-size: var(--fs-400);
						color: var(--grey);
					}
					.title {
						font-size: var(--fs-700);
					}
					.text {
						font-size: var(--fs-400);
						width: 40ch;
						font-weight: 500;
						margin: 24px 0;
					}
				}
				.image {
					display: flex;
					flex: 1;
					justify-content: center;
					img {
						max-width: 100%;
						border-radius: 25px;
						box-shadow: 4px 4px 12px 0 rgba(0, 0, 0, 0.25);
					}
				}
			}
		}
		.function-booking {
			margin: 150px 0;
			position: relative;
			width: 100%;
			.bend {
				top: -25%;
				width: 100%;
				position: absolute;
				z-index: 0;
				img {
					min-width: 100%;
				}
			}
			.content {
				position: relative;
				width: 90%;
				margin: auto;
				display: flex;
				gap: 2rem;
				.text-container {
					flex: 1;

					:global(.highlight-blue) {
						color: var(--blue-500);
						font-weight: 500;
					}
					.tag {
						font-size: var(--fs-400);
						color: var(--grey);
					}
					.title {
						font-size: var(--fs-700);
					}
					.text {
						font-size: var(--fs-400);
						width: 40ch;
						font-weight: 500;
						margin: 24px 0;
					}
				}
				.image {
					display: flex;
					flex: 1;
					justify-content: center;
					img {
						max-width: 100%;
						border-radius: 25px;
					}
				}
			}
		}

		.comparison-section {
			margin-bottom: 150px;
			display: flex;
			flex-direction: column;
			align-items: center;
			h1 {
				font-size: var(--fs-800);
				font-variation-settings: 'wght' 600;
				width: fit-content;
				margin: auto;
				width: 20ch;
				text-align: center;
				text-transform: capitalize;
				margin-bottom: 50px;
			}
			.savings-section {
				margin: 50px;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				.toggle {
					display: flex;
					p {
						font-weight: 600;
						font-size: var(--fs-600);
						margin: 0 15px;
					}
				}
				.saving-amount {
					p {
						font-weight: 500;
						font-size: var(--fs-800);
					}
				}
			}
		}

		.steps-section {
			scroll-margin-top: 150px;
			.text {
				width: 80%;
				margin: 0 auto 10vh auto;
				display: flex;
				flex-direction: column;
				align-items: center;
				.title {
					font-variation-settings: 'wght' 600;
					font-size: var(--fs-800);
					text-transform: capitalize;
				}
				.subtitle {
					font-size: var(--fs-600);
					transform: translateX(50%);
					font-variation-settings: 'wght' 500;
				}
				.subtitle::first-letter {
					text-transform: uppercase;
				}
			}
			.steps {
				display: flex;
				gap: 5%;
				justify-content: space-evenly;
				width: 80%;
				margin: auto;
			}
			.cta {
				width: fit-content;
				margin: 50px auto 0 auto;
			}
		}

		.faq-section {
			margin: 150px auto 0 auto;
			width: 100%;
			color: var(--white);
			background-color: var(--blue-700);
			display: flex;
			flex-direction: column;
			align-items: center;
			.title {
				font-variation-settings: 'wght' 600;
				font-size: var(--fs-800);
				margin: 20px auto;
			}
		}

		.ready-section {
			position: relative;
			width: 100%;
			display: flex;
			flex-direction: column;
			.front {
				// background: linear-gradient(155deg, rgba(116,171,251,1) 0%, rgba(253,253,253,1) 100%);
				border-radius: 25px;
				padding: 20px;
				width: 60%;
				// box-shadow: 5px 5px 12px 0 rgba(0, 0, 0, 0.25);
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				position: absolute;
				top: 50%;
				left: 50%;
				transform: translateX(-50%);

				.container {
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: space-evenly;
					height: 100%;
					width: fit-content;
					.title {
						margin-bottom: 16px;
						font-family: 'Roundo';
						font-size: var(--fs-700);
						font-variation-settings: 'wght' 600;
						display: flex;
						justify-content: center;
						align-items: center;
						width: 100%;
					}
					.text {
						display: flex;
						justify-content: center;
						width: 100%;
						font-size: var(--fs-600);
						font-weight: 500;

						p {
							width: 50ch;
							text-align: center;
						}
					}
					.button {
						display: flex;
						width: 100%;
						padding: 5px;
						margin: 16px 0;
						justify-content: center;
					}
				}
			}
			.back {
				width: 100%;
				img {
					min-width: 100%;
				}
			}
		}
	}

	.mobile-container {
		font-family: 'Roundo';
		:global(.highlight-white) {
			color: var(--white);
			font-weight: 600;
			font-size: calc(var(--mfs-400) + 3px);
			&::selection {
				background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
				color: #000; /* Black text for contrast */
				text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
			}
		}
		:global(.highlight-blue) {
			color: var(--blue-600);
			font-weight: 600;
			&::selection {
				background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
				color: #000; /* Black text for contrast */
				text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
			}
		}
		:global(.highlight-red) {
			color: #9c0000;
			font-weight: 600;
			&::selection {
				background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
				color: #000; /* Black text for contrast */
				text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
			}
		}

		.hero-section {
			width: 90%;
			margin: 120px auto 100px auto;
			border-radius: 100vw;
			background-image: radial-gradient(#dbdbdb 0.9px, #fdfdfd 0.9px);
			background-size: 25px 25px;

			.top {
				width: 100%;
				margin: auto;

				text-transform: capitalize;
				text-align: start;
				position: relative;
				h1 {
					font-size: var(--mfs-600);
					font-weight: 600;
				}
			}
			.bottom {
				width: 100%;
				margin: 50px 0;
				display: flex;

				p {
					font-weight: 500;
					font-size: var(--mfs-500);
					color: var(--blue-600);

					letter-spacing: 1px;
					text-transform: capitalize;
					text-align: start;
					display: flex;
					width: 100%;
				}
				.reviewers {
					justify-content: center;
					align-items: center;
					display: flex;
					width: 100%;
				}
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
		.process-section {
			margin: 100px 0 0 0;
			background-color: var(--blue-700);
			width: 100%;
			padding-bottom: clamp(12.5rem, 6.2396rem + 25.0417vw, 21.875rem);
			position: relative;

			display: flex;
			flex-direction: column;

			color: var(--white);

			.title {
				width: 100%;
				text-align: center;
				padding: 20px;
				h1 {
					font-weight: 500;
					font-size: var(--mfs-600);
				}
			}
			.text {
				width: 100%;
				text-align: center;
				display: flex;
				justify-content: center;
				p {
					max-width: 40ch;
					font-size: var(--mfs-400);
				}
			}
			.illustration {
				position: absolute;
				top: clamp(9.375rem, 5.2014rem + 16.6945vw, 15.625rem);
				width: clamp(20rem, 12.4875rem + 30.0501vw, 31.25rem);
				left: 50%;
				transform: translateX(-50%);
				img {
					max-width: 100%;
					max-height: 100%;
				}
			}
		}
		.review-section {
			margin-bottom: 50px;
			padding: 25px 0;
			background-color: var(--blue-300);
			.stats {
				ul {
					font-family: 'Sfpro';
					padding-top: clamp(6.25rem, 2.0764rem + 16.6945vw, 12.5rem);
					display: flex;
					align-items: center;
					justify-content: space-evenly;
					color: var(--grey);
					li {
						width: 10ch;
						margin: 10px 0;
						list-style-type: none;
						h1 {
							text-align: center;
							font-weight: 600;
							font-size: var(--mfs-600);
						}
						p {
							text-align: center;
						}
					}
				}
			}
			.review-carousel {
				scroll-margin-top: 250px;
				margin-top: 50px;
				width: 100%;
			}
		}

		.function-ads {
			margin: 100px 0;
			max-width: 100%;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			.container {
				width: 90%;
				margin: auto;
				display: flex;
				flex-direction: column;

				.title {
					:global(.highlight-blue) {
						color: var(--blue-500);
						font-weight: 500;
						font-size: var(--mfs-600);
					}
					.tag {
						font-size: var(--mfs-400);
						color: var(--grey);
					}
					.title {
						font-size: var(--mfs-600);
					}
				}
				.content {
					display: flex;
					justify-content: center;
					.text {
						font-size: var(--mfs-400);
						font-weight: 500;
						margin: 24px 0;
						flex: 1;
					}
					img {
						flex: 1;
						max-height: 100%;
						max-width: 50%;
					}
				}
			}
		}

		.function-landingpage {
			margin: 100px 0;
			position: relative;
			z-index: 5;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			.content {
				width: 90%;
				margin: auto;
				display: flex;
				gap: 2rem;
				display: flex;
				flex-direction: column;
				.text-container {
					flex: 1;

					:global(.highlight-blue) {
						color: var(--blue-500);
						font-weight: 500;
						font-size: var(--mfs-600);
					}
					.tag {
						font-size: var(--fs-500);
						color: var(--grey);
					}
					.title {
						font-size: var(--mfs-600);
					}
					.text {
						font-size: var(--fs-500);
						font-weight: 500;
						margin: 24px 0 0 0;
					}
				}
				.image {
					display: flex;
					flex: 1;
					justify-content: center;
					margin: 24px 0;
					img {
						max-width: 100%;
						border-radius: 25px;
						box-shadow: 4px 4px 12px 0 rgba(0, 0, 0, 0.25);
					}
				}
			}
		}

		.function-booking {
			margin: 150px 0;
			position: relative;
			width: 100%;
			overflow-x: clip;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			.bend {
				top: -5%;
				width: 100%;
				height: 200%;
				position: absolute;
				z-index: 0;
				img {
					min-width: 100%;
				}
			}
			.content {
				position: relative;
				width: 90%;
				margin: 0 auto 24px auto;
				display: flex;
				flex-direction: column;
				gap: 2rem;
				.text-container {
					flex: 1;

					:global(.highlight-blue) {
						color: var(--blue-500);
						font-weight: 500;
						font-size: var(--mfs-600);
					}
					.tag {
						font-size: var(--mfs-500);
						color: var(--grey);
					}
					.title {
						font-size: var(--mfs-600);
					}
					.text {
						font-size: var(--mfs-500);
						font-weight: 500;
						margin: 24px 0;
					}
				}
				.image {
					display: flex;
					flex: 1;
					justify-content: center;
					img {
						max-width: 100%;
						border-radius: 25px;
					}
				}
			}
		}

		.comparison-section {
			margin-bottom: 50px;
			display: flex;
			flex-direction: column;
			align-items: center;
			h1 {
				font-size: var(--mfs-600);
				font-variation-settings: 'wght' 600;
				width: fit-content;
				margin: auto;
				text-align: center;
				text-transform: capitalize;
			}
			.savings-section {
				margin: 5px;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				.toggle {
					display: flex;
					p {
						font-weight: 600;
						font-size: var(--fs-600);
						margin: 0 15px;
					}
				}
				.saving-amount {
					p {
						text-align: center;
						font-weight: 500;
						font-size: var(--mfs-600);
					}
				}
			}
		}

		.steps-section {
			scroll-margin-top: 250px;
			.text {
				width: 90%;
				margin: 0 auto 32px auto;
				display: flex;
				flex-direction: column;
				align-items: center;
				.title {
					font-variation-settings: 'wght' 600;
					font-size: var(--mfs-600);
					text-transform: capitalize;
				}
				.subtitle {
					margin-top: 16px;
					font-size: var(--mfs-400);
					font-variation-settings: 'wght' 500;
				}
				.subtitle::first-letter {
					text-transform: uppercase;
				}
			}
			.steps {
				display: flex;
				flex-direction: column;
				gap: 20px;
				width: 90%;
				margin: auto;
			}
			.cta {
				width: fit-content;
				margin: 50px auto 0 auto;
			}
		}

		.faq-section {
			margin: 100px auto 0 auto;
			width: 100%;
			color: var(--white);
			background-color: var(--blue-700);
			display: flex;
			flex-direction: column;
			align-items: center;
			.title {
				font-variation-settings: 'wght' 600;
				font-size: var(--mfs-600);
				margin: 20px auto;
			}
		}

		.ready-section {
			position: relative;
			width: 100%;
			display: flex;
			flex-direction: column;
			.front {
				// background: linear-gradient(155deg, rgba(116,171,251,1) 0%, rgba(253,253,253,1) 100%);
				border-radius: 25px;
				padding: 20px;
				width: 90%;
				// box-shadow: 5px 5px 12px 0 rgba(0, 0, 0, 0.25);
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				position: absolute;
				top: 50%;
				left: 50%;
				transform: translateX(-50%);

				.container {
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: space-evenly;
					height: 100%;
					width: 100%;
					.title {
						margin-bottom: 16px;
						font-family: 'Roundo';
						font-size: var(--mfs-600);
						font-variation-settings: 'wght' 600;
						display: flex;
						justify-content: center;
						align-items: center;
						text-align: center;
						width: 100%;
					}
					.text {
						display: flex;
						justify-content: center;
						width: 100%;
						font-size: var(--mfs-500);
						font-weight: 500;

						p {
							text-align: center;
						}
					}
					.button {
						display: flex;
						width: 100%;
						padding: 5px;
						margin: 16px 0;
						justify-content: center;
					}
				}
			}
			.back {
				width: 100%;
				img {
					min-width: 100%;
					max-width: 100%;
				}
			}
		}
	}
</style>
