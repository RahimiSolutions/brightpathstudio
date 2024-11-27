<script lang="ts">
	import { onMount } from 'svelte';
	import { flip } from 'svelte/animate';
	import { fade } from 'svelte/transition';

	import logo from '$lib/images/logo-nostudio.png';
	import Calendar from '$lib/icons/calendar.svelte';
	import Automation from '$lib/icons/automation.svelte';
	import Computer from '$lib/icons/computer.svelte';
	import Email from '$lib/icons/email.svelte';
	import Offer from '$lib/icons/offer.svelte';
	import People from '$lib/icons/people.svelte';
	import Survey from '$lib/icons/survey.svelte';
	import Slider from './slider.svelte';
	import { t } from '$lib/text/i18n';

	export let feature;
	export let flipped = false;
	let selectedYearIndex = 0;
	$: months = selectedYearIndex * 12 + 12;

	function handleMouseClick() {
		flipped = !flipped;
	}

	function getIcon(iconName: any) {
		switch (iconName) {
			case 'calendar':
				return Calendar;
			case 'automation':
				return Automation;
			case 'computer':
				return Computer;
			case 'email':
				return Email;
			case 'offer':
				return Offer;
			case 'people':
				return People;
			case 'survey':
				return Survey;
			default:
				return null;
		}
	}

</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<!-- svelte-ignore a11y_click_events_have_key_events -->
<div class="card" on:click={handleMouseClick} class:flipped>
	<div class="card-front">
		<div class="icon">
			{#if feature.icon}
				<svelte:component this={getIcon(feature.icon)} />
			{/if}
		</div>
		<p class="title">{feature.title}</p>
		<p class="description">{feature.description}</p>
		<p class="replaced-tool">{@html $t('replacing')}: {feature.replacedTool}</p>
		<button class="cta">
			<span>{@html $t('flip-prompt')}</span>
			<svg width="15px" height="10px" viewBox="0 0 13 10">
			  <path d="M1,5 L11,5"></path>
			  <polyline points="8 1 12 5 8 9"></polyline>
			</svg>
		  </button>
	</div>

	<div class="card-back">
		<!-- <p class="title">Price Comparison</p> -->
		<div class="container">
			<div class="others">
				<div class="tag">
					<p>{@html $t('others')}</p>
					<p>{@html $t('cost-after')} {selectedYearIndex + 1} {@html $t('year')}</p>
				</div>
				<div class="content">
					<div class="monthly-price">{@html $t('usd-sign')}{feature.marketPrice}{@html $t('nok-sign')}/{@html $t('month')}</div>
					<div class="annual-expense">- {@html $t('usd-sign')}{feature.marketPrice * months}{@html $t('nok-sign')}</div>
				</div>
			</div>
			<div class="brightpath">
				<div class="tag">
					<img src={logo} alt="" />
					<p>{@html $t('saved-after')} {selectedYearIndex + 1} {@html $t('year')}</p>
				</div>
				<div class="content">
					<div class="included">{@html $t('included')}</div>
					<div class="annual-saved">+ {@html $t('usd-sign')}{feature.marketPrice * months}{@html $t('nok-sign')}</div>
				</div>
			</div>
		</div>
		<div class="slider" on:click|stopPropagation>
			<Slider bind:selectedYearIndex />
		</div>
	</div>
</div>

<style lang="scss">
	::selection {
		background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
		color: #000; /* Black text for contrast */
		text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
	}
	.cta {
		right: 10px;
		bottom: 10px;
		position: absolute;
		margin: auto;
		padding: 12px 18px;
		transition: all 0.2s ease;
		border: none;
		background: none;
		cursor: pointer;
	}

	.cta:before {
		content: '';
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		left: 0;
		display: block;
		border-radius: 50px;
		background: var(--blue-300);
		width: 28px;
		height: 28px;
		transition: all 0.3s ease;
	}

	.cta span {
		font-family: "Sfpro";
		position: relative;
		font-size: var(--fs-300);
		font-weight: 700;
		letter-spacing: 0.05em;
		color: var(--blue-600);
	}

	.cta svg {
		position: relative;
		top: 0;
		margin-left: 10px;
		fill: none;
		stroke-linecap: round;
		stroke-linejoin: round;
		stroke: var(--blue-600);
		stroke-width: 2;
		transform: translateX(-5px);
		transition: all 0.3s ease;
	}

	.card:hover .cta:before {
		width: 100%;
		background: var(--blue-300);
	}

	.card:hover svg {
		transform: translateX(0);
	}

	.card:active {
		transform: scale(0.95);
	}

	.card {
		position: relative;
		background: transparent; /* Background on the card is set to transparent */
		width: 350px;
		height: 350px;
		perspective: 1000px; /* Enables 3D effect */
		cursor: pointer;
		transition: transform 0.3s ease;
		&:hover {
			transform: translateY(-5px);
		}

		&.flipped .card-front {
			transform: rotateY(180deg); /* Flip the front side when flipped */
		}

		&.flipped .card-back {
			transform: rotateY(0deg); /* Show the back side when flipped */
		}
		.title {
			color: var(--black);
			font-size: var(--fs-600);
			font-weight: 600;
		}

		.card-front,
		.card-back {
			position: absolute;
			width: 100%;
			height: 100%;
			backface-visibility: hidden; /* Hide the back when flipped */
			transition: transform 0.6s cubic-bezier(0.4, 0.2, 0.2, 1); /* Smooth flipping animation */
			box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
			border-radius: 12px;
		}

		.card-front {
			background: white;
			transform: rotateY(0deg); /* Default position for the front side */
			display: flex;
			flex-direction: column;
			align-items: center;
			padding: 20px;
			box-sizing: border-box;

			.title{
				text-align: center;
				margin-bottom: 8px;
			}
			.icon {
				margin-bottom: 1em;
			}

			.description {
				margin-bottom: 1em;
				width: 100%;
				text-align: start;
				color: var(--black);
				font-size: var(--fs-400);
				font-weight: 500;
			}

			.replaced-tool {
				width: 100%;
				text-align: start;
				font-style: italic;
				color: var(--grey);
				margin-bottom: 1em;
			}

			.savings {
				position: absolute;
				right: 20px;
				bottom: 20px;

				width: 100%;
				text-align: end;
				color: var(--black);
				font-weight: 500;
				font-size: 0.9em;
			}
		}

		.card-back {
			background: white;
			transform: rotateY(-180deg); /* Initially hide the back side */

			display: flex;
			flex-direction: column;
			justify-content: space-evenly;
			align-items: center;
			padding: 20px;
			box-sizing: border-box;
			.slider {
				width: 95%;
			}
			.container {
				width: 100%;
				display: flex;
				flex-direction: column;
				gap: 36px;

				.others {
					width: 100%;

					.tag {
						font-size: var(--fs-300);
						color: var(--grey);
						font-weight: 500;
						display: flex;
						justify-content: space-between;
						margin-bottom: 5px;
					}

					.content {
						width: 100%;
						display: flex;
						justify-content: space-between;
						align-items: baseline;

						.monthly-price {
							font-weight: 500;
							font-size: var(--fs-600);
						}

						.annual-expense {
							color: var(--red);
							font-weight: 500;
							font-size: var(--fs-600);
						}
					}
				}

				.brightpath {
					width: 100%;

					.tag {
						color: var(--grey);
						height: var(--fs-300);
						font-size: var(--fs-300);
						font-weight: 500;
						display: flex;
						justify-content: space-between;
						margin-bottom: 5px;

						img {
							max-height: 100%;
							opacity: 0.8;
						}
					}

					.content {
						width: 100%;
						display: flex;
						justify-content: space-between;
						align-items: baseline;

						.included {
							font-size: 24px;
							font-weight: 500;
							font-size: var(--fs-600);
						}

						.annual-saved {
							color: var(--green);
							font-weight: 500;
							font-size: var(--fs-600);
						}
					}
				}
			}
		}
	}
</style>
