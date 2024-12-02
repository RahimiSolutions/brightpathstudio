<script lang="ts">
	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';
	import Chevron from '$lib/icons/Chevron.svelte';

	import reviwerOne from '$lib/images/reviewerOne.png';
	import reviwerTwo from '$lib/images/reviewerTwo.png';
	import reviwerThree from '$lib/images/reviewerThree.png';
	import { t } from '$lib/text/i18n';
	let reviewOne = $t('reviewOne');
	let reviewTwo = $t('reviewTwo');
	let reviewThree = $t('reviewThree');

	const reviews = [
		{ image: reviwerOne, text: reviewOne, name: 'John Doe', company: 'Doe Inc.' },
		{ image: reviwerTwo, text: reviewTwo, name: 'Jane Smith', company: 'Smith & Co.' },
		{ image: reviwerThree, text: reviewThree, name: 'Elliot Brown', company: 'Brown Ltd.' }
		// Add more reviews as needed
	];

	let currentIndex = 0;

	function showNext() {
		currentIndex = (currentIndex + 1) % reviews.length;
	}

	function showPrevious() {
		currentIndex = (currentIndex - 1 + reviews.length) % reviews.length;
	}
</script>

<!-- svelte-ignore a11y_click_events_have_key_events a11y_no_static_element_interactions -->
<div class="carousel-container">
	<div class="content">
		<div class="arrow arrow-left" on:click={showPrevious}>
			<Chevron width="24" />
		</div>
		<div class="review-card">
			<div class="profile-image">
				<img src={reviews[currentIndex].image} alt={reviews[currentIndex].name} />
			</div>
			<div class="review-content">
				<p class="review-text" transition:fly={{ x: 100, duration: 300 }}>
					{reviews[currentIndex].text}
				</p>
				<div class="reviewer-info">
					<p class="name">{reviews[currentIndex].name}</p>
					<p class="company">{reviews[currentIndex].company}</p>
				</div>
			</div>
		</div>
		<div class="arrow arrow-right" on:click={showNext}>
			<Chevron width="24" />
		</div>
	</div>

	<div class="indicator-container">
		{#each reviews as _, index}
			<div
				class="indicator {index === currentIndex ? 'active' : ''}"
				on:click={() => (currentIndex = index)}
			></div>
		{/each}
	</div>
</div>

<style lang="scss">
	.carousel-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		position: relative;
		width: 100%;
		max-width: 600px;
		margin: auto;
		padding: 20px;
		.content {
			display: flex;
			justify-content: space-evenly;
			align-items: center;
			.arrow {
				cursor: pointer;
				color: var(--blue-600);
				user-select: none;

				&.arrow-left {
					-webkit-transform: scaleX(-1);
					transform: scaleX(-1);
				}
			}

			.review-card {
				display: flex;
				width: 100%;
				max-width: 100%;
				justify-content: space-between;
				align-items: center;
				padding: 10px;
				border-radius: 10px;

				.profile-image {
					width: 80px;
					height: 80px;
					border-radius: 50%;
					overflow: hidden;
					flex-shrink: 0;

					img {
						width: 100%;
						height: 100%;
						object-fit: cover;
						transition: transform 0.3s ease-in-out;

						&:hover {
							transform: scale(1.1);
						}
					}
				}

				.review-content {
					flex-grow: 1;
					display: flex;
					flex-direction: column;
					justify-content: space-between;
					padding-left: 20px;
					gap: 20px;

					.review-text {
						font-size: var(--fs-500);
						color: var(--font-color);
						font-weight: 500;
						width: 100%;
					}

					.reviewer-info {
						text-align: right;

						.name {
							font-size: var(--fs-600);
							font-weight: 600;
							color: var(--blue-600);
						}

						.company {
							font-size: var(--fs-400);
							font-weight: 500;
						}
					}
				}
			}
		}

		.indicator-container {
			display: flex;
			gap: 10px;
			margin-top: 20px;

			.indicator {
				width: 10px;
				height: 10px;
				background: var(--blue-600);
				border-radius: 50%;
				cursor: pointer;
				opacity: 0.5;
				transition: opacity 0.3s ease-in-out;

				&.active {
					opacity: 1;
					background: var(--blue-700);
				}
			}
		}
	}
</style>
