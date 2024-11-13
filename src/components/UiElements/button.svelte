<script>
	import { goto } from '$app/navigation';
	import { t } from '$lib/text/i18n';

	let { fontsize = '1em', text = 'text', link = '' } = $props();

	function goToLink() {
		if (link) {
			if (link.startsWith('http://') || link.startsWith('https://')) {
				// External link: Use window.location for external navigation
				window.location.href = link;
			} else {
				// Internal link: Use SvelteKit's goto function for internal navigation
				goto(link);
			}
		}
	}
</script>

<button onclick={goToLink}>
	<div class="container">
		{@html $t('cta')}
	</div>
</button>

<style lang="scss">
	::selection {
		background: #fff; 
		color:rgba(0, 123, 255, 1);  
		text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5);
	}
	button {
		position: relative;
		padding: 20px 30px;
		border: none;
		border-radius: 10px;
		background-color: var(--blue-500);
		color: var(--white);
		font-size: var(--fs-600);
		font-weight: 600;
		font-family: 'Roundo';
		cursor: pointer;
		transition:
			transform 0.3s ease-in-out,
			box-shadow 0.3s ease-in-out;

		/* Initial box shadow (inset + outer shadow) */
		box-shadow:
			inset 0 4px 12px rgba(255, 255, 255, 0.6),
			/* Inset shadow */ 0 4px 6px rgba(0, 0, 0, 0.2); /* Outer shadow */

		&:hover {
			transform: translate(-3px, -3px);
			/* Adjust the outer shadow to appear as if it's being left behind */
			box-shadow:
				inset 0 4px 12px rgba(255, 255, 255, 0.6),
				/* Inset shadow remains */ 6px 6px 0 rgba(0, 0, 0, 0.6); /* Shadow left behind */
		}
	}
</style>
