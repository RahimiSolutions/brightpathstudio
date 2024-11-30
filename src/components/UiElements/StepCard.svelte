<script>
	import MediaQuery from '../MediaQuery.svelte';

	let { number, title, text } = $props();
</script>

<MediaQuery query="(min-width: 721px)" let:matches>
	{#if matches}
		<article class="card">
			<div class="header">
				<div class="number"><h1>{number}</h1></div>
				<div class="title"><h1>{title}</h1></div>
			</div>
			<div class="text"><p>{@html text}</p></div>
		</article>
	{/if}
</MediaQuery>
<MediaQuery query="(max-width: 720px)" let:matches>
	{#if matches}
		<article class="mobile-card">
			<div class="left">
				<div class="number"><h1>{number}</h1></div>
			</div>
			<div class="right">
				<div class="title"><h1>{title}</h1></div>
				<p>{@html text}</p>
			</div>
		</article>
	{/if}
</MediaQuery>

<style lang="scss">
	::selection {
		background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
		color: #000; /* Black text for contrast */
		text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
	}
	.card {
		font-family: 'Sfpro';
		width: 100%;
		border-radius: 15px;
		background-color: var(--blue-300);
		box-shadow: 4px 4px 8px 0 rgba(0, 0, 0, 0.25);
		padding: 15px;
		.header {
			display: flex;
			gap: 10px;
			align-items: baseline;
			.number {
				width: 50px;
				font-family: 'Roundo';
				font-size: clamp(2rem, -1.2609rem + 5.2174vw, 5rem);
				font-variation-settings: 'wght' 500;
				color: transparent;
				text-shadow:
					2px 2px 3px var(--white),
					0px 0px 0px rgba(0, 0, 0, 0.25);

				h1 {
				}
			}
			.title {
				font-size: clamp(1.5rem, 0.413rem + 1.7391vw, 2.5rem);
				font-variation-settings: 'wght' 400;
				h1 {
					text-transform: capitalize;
					color: var(--black);
				}
			}
		}
		.text {
			margin: 0 0 40px 60px;
			p {
				font-size: clamp(1rem, 0.4565rem + 0.8696vw, 1.5rem);
				color: var(--black);
			}
		}
	}
	.mobile-card {
		font-family: 'Sfpro';
		width: 100%;
		border-radius: 15px;
		background-color: var(--blue-300);
		box-shadow: 4px 4px 8px 0 rgba(0, 0, 0, 0.25);
		padding: 15px;
		display: flex;
		gap: 10px;
		.left {
			width: 20%;
			.number {
				
				font-family: 'Roundo';
				font-size: clamp(6.125rem, 5.2068rem + 3.6728vw, 7.5rem);
				font-variation-settings: 'wght' 500;
				color: transparent;
				text-shadow:
					2px 2px 3px var(--white),
					0px 0px 0px rgba(0, 0, 0, 0.25);

				h1 {
				}
			}
		}
		.right {
			width: 80%;
			display: flex;
			flex-direction: column;
			justify-content: center;
			.title {
				font-size: var(--mfs-600);
				font-variation-settings: 'wght' 400;
				margin-bottom: 8px;
				h1 {
					text-transform: capitalize;
					color: var(--black);
				}
			}
			p {
				font-size: var(--mfs-400);
				color: var(--black);
			}
		}
	}
</style>
