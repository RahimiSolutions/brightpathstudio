<script lang="ts">
	import { flip } from 'svelte/animate';
	import ComparisonCard from './ComparisonCard.svelte';
	import { t } from '$lib/text/i18n';
	import MediaQuery from '../MediaQuery.svelte';

	let bookingTitle = $t('booking-system-title');
	let bookingDescription = $t('booking-system-description');
	let bookingPrice = $t('booking-system-price');

	let landingPageTitle = $t('landingpage-title');
	let landingPageDescription = $t('landingpage-description');
	let landingPagePrice = $t('landingpage-price');

	let crmPipelineTitle = $t('crm-pipeline-title');
	let crmPipelineDescription = $t('crm-pipeline-description');
	let crmPipelinePrice = $t('crm-pipeline-price');

	let emailMarketingTitle = $t('email-marketing-title');
	let emailMarketingDescription = $t('email-marketing-description');
	let emailMarketingPrice = $t('email-marketing-price');

	let formsSurveysTitle = $t('forms-surveys-title');
	let formsSurveysDescription = $t('forms-surveys-description');
	let formsSurveysPrice = $t('forms-surveys-price');

	let automationsTitle = $t('automations-title');
	let automationsDescription = $t('automations-description');
	let automationsPrice = $t('automations-price');

	let offersESignaturesTitle = $t('offers-esignatures-title');
	let offersESignaturesDescription = $t('offers-esignatures-description');
	let offersESignaturesPrice = $t('offers-esignatures-price');

	let features = [
		{
			id: 1,
			title: bookingTitle,
			replacedTool: 'Calendly, Bookingtjeneste',
			icon: 'calendar',
			width: '80',
			description: bookingDescription,
			marketPrice: bookingPrice
		},
		{
			id: 2,
			title: landingPageTitle,
			replacedTool: 'Wix, Clickfunnels',
			icon: 'computer',
			width: '80',
			description: landingPageDescription,
			marketPrice: landingPagePrice
		},
		{
			id: 3,
			title: crmPipelineTitle,
			replacedTool: 'Salesforce, HubSpot',
			icon: 'people',
			width: '80',
			description: crmPipelineDescription,
			marketPrice: crmPipelinePrice
		},
		{
			id: 4,
			title: emailMarketingTitle,
			replacedTool: 'Mailchimp, Constant Contact',
			icon: 'email',
			width: '80',
			description: emailMarketingDescription,
			marketPrice: emailMarketingPrice
		},
		{
			id: 5,
			title: formsSurveysTitle,
			replacedTool: 'Google Forms, SurveyMonkey',
			icon: 'survey',
			width: '80',
			description: formsSurveysDescription,
			marketPrice: formsSurveysPrice
		},
		{
			id: 6,
			title: automationsTitle,
			replacedTool: 'Zapier, IFTTT',
			icon: 'automation',
			width: '80',
			description: automationsDescription,
			marketPrice: automationsPrice
		},
		{
			id: 7,
			title: offersESignaturesTitle,
			replacedTool: 'DocuSign, HelloSign',
			icon: 'offer',
			width: '80',
			description: offersESignaturesDescription,
			marketPrice: offersESignaturesPrice
		}
	];
</script>

<MediaQuery query="(min-width: 721px)" let:matches>
	{#if matches}
		<div class="card-container">
			{#each features as feature (feature.id)}
				<div animate:flip={{ duration: 300 }}>
					<ComparisonCard {feature} />
				</div>
			{/each}
		</div>
	{/if}
</MediaQuery>
<MediaQuery query="(max-width: 720px)" let:matches>
	{#if matches}
		<div class="mobile-card-container">
			{#each features as feature (feature.id)}
				<div animate:flip={{ duration: 300 }}>
					<ComparisonCard {feature} />
				</div>
			{/each}
		</div>
	{/if}
</MediaQuery>

<style lang="scss">
	.card-container {
		width: 80%;
		margin: 10px auto;
		display: flex;
		flex-wrap: wrap; /* Allow items to wrap onto the next line */
		justify-content: center; /* Center items horizontally */
		gap: 20px;
		padding: 20px;

		.card-container > div {
			margin-bottom: 20px;
			flex: 0 0 calc(25% - 20px); /* Set each card to take up 25% of the container width minus gap */
			box-sizing: border-box; /* Ensure padding is included in width calculation */
		}
	}
	.mobile-card-container {
		width: 90%;
		margin: 24px 0;
		display: flex;
		flex-direction: column;
		justify-content: center; /* Center items horizontally */
		align-items: center;
		gap: 20px;

		// .card-container > div {
		// 	margin-bottom: 20px;
		// 	flex: 0 0 calc(25% - 20px); /* Set each card to take up 25% of the container width minus gap */
		// 	box-sizing: border-box; /* Ensure padding is included in width calculation */
		// }
	}
</style>
