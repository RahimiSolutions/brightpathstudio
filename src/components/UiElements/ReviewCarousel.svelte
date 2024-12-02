<script>
	import reviwerOne from '$lib/images/reviewerOne.png';
	import reviwerTwo from '$lib/images/reviewerTwo.png';
	import reviwerThree from '$lib/images/reviewerThree.png';
	import { t } from '$lib/text/i18n';
	let reviewOne = $t('reviewOne');
	let reviewTwo = $t('reviewTwo');
	let reviewThree = $t('reviewThree');

	const reviews = [
		{ name: 'John Doe', company: 'Nexis Solutions', body: reviewOne, img: reviwerOne },
		{ name: 'Jane Smith', company: 'GreenLeaf Organics', body: reviewTwo, img: reviwerTwo },
		{ name: 'Elliot Brown', company: 'UrbanNest Designs', body: reviewThree, img: reviwerThree },
		{ name: 'John Doe', company: 'Nexis Solutions', body: reviewOne, img: reviwerOne },
		{ name: 'Jane Smith', company: 'GreenLeaf Organics', body: reviewTwo, img: reviwerTwo },
		{ name: 'Elliot Brown', company: 'UrbanNest Designs', body: reviewThree, img: reviwerThree }
	];
	

	const firstRow = reviews.slice(0, reviews.length / 2);
	const secondRow = reviews.slice(reviews.length / 2);
	let isPaused = false;

	function pauseAnimation() {
		isPaused = true;
	}

	function resumeAnimation() {
		isPaused = false;
	}
</script>

<!-- svelte-ignore a11y_no_static_element_interactions a11y_figcaption_parent -->
<div class="carousel">
	<div class="marquee" on:mouseenter={pauseAnimation} on:mouseleave={resumeAnimation}>
		<div class="track" class:paused={isPaused}>
			{#each [...firstRow, ...firstRow, ...firstRow] as review}
				<div class="review-card">
					<div class="profile">
						<img src={review.img} alt="" />
						<div class="info">
							<figcaption>{review.name}</figcaption>
							<p>{review.company}</p>
						</div>
					</div>
					<blockquote>{review.body}</blockquote>
				</div>
			{/each}
		</div>
	</div>

	<div class="marquee reverse" on:mouseenter={pauseAnimation} on:mouseleave={resumeAnimation}>
		<div class="track" class:paused={isPaused}>
			{#each [...secondRow, ...secondRow, ...secondRow] as review}
				<div class="review-card">
					<div class="profile">
						<img src={review.img} alt="" />
						<div class="info">
							<figcaption>{review.name}</figcaption>
							<p>{review.company}</p>
						</div>
					</div>
					<blockquote>{review.body}</blockquote>
				</div>
			{/each}
		</div>
	</div>
	<div class="fade left"></div>
	<div class="fade right"></div>
</div>

<style lang="scss">
	::selection {
		background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
		color: #000; /* Black text for contrast */
		text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
	}
	.carousel {
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: center;
		overflow: hidden;
		height: fit-content;
		background-color: var(--blue-200);
		

		.marquee {
			position: relative;
			width: 100%;
			height: 200px;
			display: flex;
			align-items: center;
			overflow: hidden;

			.track {
				display: flex;
				position: absolute;
				white-space: nowrap;
				will-change: transform;
				animation: marquee 30s linear infinite; // Increased duration for smoother effect

				&.paused {
					animation-play-state: paused;
				}
			}

			&.reverse .track {
				animation-direction: reverse;
			}
		}

		@keyframes marquee {
			0% {
				transform: translateX(0);
			}
			100% {
				transform: translateX(-33.33%); // Move by 1/3 of the total width
			}
		}

		.review-card {
			display: inline-block;
			width: 20vw;
			max-width: 300px;
			min-width: 200px;
			padding: 1rem;
			margin-right: 2rem;
			background-color: rgba(255, 255, 255, 0.9);
			border: 1px solid rgba(0, 0, 0, 0.1);
			border-radius: 10px;
			transition: background-color 0.3s ease;
			cursor: pointer;

			&:hover {
				background-color: rgba(255, 255, 255, 1);
			}

			.profile {
				display: flex;
				align-items: center;
				gap: 1rem;
				margin-bottom: 0.5rem;

				img {
					width: 48px;
					height: 48px;
					border-radius: 50%;
				}

				.info {
					display: flex;
					flex-direction: column;

					figcaption {
						font-weight: bold;
						font-size: 1rem;
					}

					p {
						font-size: 0.9rem;
						color: #666;
					}
				}
			}

			blockquote {
				font-size: 1rem;
				color: #333;
				line-height: 1.4;
				margin-top: 0.5rem;
				white-space: normal;
			}
		}

		.fade {
			position: absolute;
			top: 0;
			bottom: 0;
			width: 15%;
			pointer-events: none;

			&.left {
				left: 0;
				background: linear-gradient(to right, var(--white), transparent);
			}

			&.right {
				right: 0;
				background: linear-gradient(to left, var(--white), transparent);
			}
		}
	}
</style>
