<script lang="ts">
	import { slide } from 'svelte/transition';
	import { t } from '$lib/text/i18n';
	import MediaQuery from '../MediaQuery.svelte';

	const faqs = [
		{ question: 'faq-one-question', answer: 'faq-one-answer' },
		{ question: 'faq-two-question', answer: 'faq-two-answer' },
		{ question: 'faq-three-question', answer: 'faq-three-answer' },
		{ question: 'faq-four-question', answer: 'faq-four-answer' },
		{ question: 'faq-five-question', answer: 'faq-five-answer' },
		{ question: 'faq-six-question', answer: 'faq-six-answer' },
		{ question: 'faq-seven-question', answer: 'faq-seven-answer' }
	];

	let activeIndex: number | null = null;

	function toggle(index: number) {
		activeIndex = activeIndex === index ? null : index;
	}
</script>

<MediaQuery query="(min-width: 721px)" let:matches>
	{#if matches}
		<div class="faq-container">
			{#each faqs as { question, answer }, index}
				<div class="faq-item" class:active={activeIndex === index}>
					<button
						class="faq-question"
						on:click={() => toggle(index)}
						aria-expanded={activeIndex === index}
					>
						<span class="question-text">{@html $t(question)}</span>
						<span class="icon">{activeIndex === index ? '−' : '+'}</span>
					</button>

					{#if activeIndex === index}
						<div class="faq-answer" transition:slide={{ duration: 300 }}>
							{@html $t(answer)}
						</div>
					{/if}
				</div>
			{/each}
		</div>
	{/if}
</MediaQuery>
<MediaQuery query="(max-width: 720px)" let:matches>
	{#if matches}
		<div class="mobile-faq-container">
			{#each faqs as { question, answer }, index}
				<div class="faq-item" class:active={activeIndex === index}>
					<button
						class="faq-question"
						on:click={() => toggle(index)}
						aria-expanded={activeIndex === index}
					>
						<span class="question-text">{@html $t(question)}</span>
						<span class="icon">{activeIndex === index ? '−' : '+'}</span>
					</button>

					{#if activeIndex === index}
						<div class="faq-answer" transition:slide={{ duration: 300 }}>
							{@html $t(answer)}
						</div>
					{/if}
				</div>
			{/each}
		</div>
	{/if}
</MediaQuery>

<style lang="scss">
	::selection {
		background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
		color: #000; /* Black text for contrast */
		text-shadow: 0 1px 1px rgba(0, 0, 0, 0.5); /* Subtle white shadow for depth */
	}
	.faq-container {
		font-family: 'Roundo', sans-serif;
		max-width: 800px;
		width: 100%;
		margin: 2rem auto;
		padding: 2rem 1rem;
		background-color: var(--blue-700, #124fa9);
		border-radius: 12px;

		.faq-item {
			background-color: rgba(255, 255, 255, 0.05);
			border-radius: 8px;
			margin-bottom: 1rem;
			transition: all 0.3s ease;

			&:hover {
				background-color: rgba(255, 255, 255, 0.1);
			}

			&.active {
				background-color: #ffffff;
				box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

				.faq-question {
					color: var(--blue-700, #124fa9);
				}
			}

			.faq-question {
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
				color: #ffffff;
				transition: color 0.3s ease;

				.question-text {
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

			.faq-answer {
				padding: 0 1rem 1rem;
				font-family: 'Sfpro', sans-serif;
				font-size: var(--fs-400);
				line-height: 1.6;
				color: var(--blue-700, #124fa9);
			}
		}
	}
	.mobile-faq-container {
		font-family: 'Roundo', sans-serif;
		max-width: 800px;
		width: 100%;
		margin: 1rem auto;
		padding: 2rem 1rem;
		background-color: var(--blue-700, #124fa9);
		border-radius: 12px;

		.faq-item {
			background-color: rgba(255, 255, 255, 0.05);
			border-radius: 8px;
			margin-bottom: 1rem;
			transition: all 0.3s ease;

			&:hover {
				background-color: rgba(255, 255, 255, 0.1);
			}

			&.active {
				background-color: #ffffff;
				box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

				.faq-question {
					color: var(--blue-700, #124fa9);
				}
			}

			.faq-question {
				background: none;
				border: none;
				cursor: pointer;
				display: flex;
				justify-content: space-between;
				align-items: center;
				width: 100%;
				padding: 1.25rem;
				font-family: inherit;
				font-size: var(--mfs-500);
				font-weight: 500;
				color: #ffffff;
				transition: color 0.3s ease;

				.question-text {
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

			.faq-answer {
				padding: 0 1rem 1rem;
				font-family: 'Sfpro', sans-serif;
				font-size: var(--mfs-400);
				line-height: 1.6;
				color: var(--blue-700, #124fa9);
			}
		}
	}
</style>
