<script>
	let { number, title, text } = $props();
</script>

<article class="card">
	<div class="header">
		<div class="number"><h1>{number}</h1></div>
		<div class="title"><h1>{title}</h1></div>
	</div>
	<div class="text"><p>{@html text}</p></div>
</article>

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
</style>
