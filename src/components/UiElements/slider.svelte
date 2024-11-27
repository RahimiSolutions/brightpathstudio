<script lang="ts">
	import { onMount } from 'svelte';

	let currentYear: number;
	let years: number[] = [];
	export let selectedYearIndex = 0;
	let numYears = 7; // Number of years to display, including the current year

	onMount(() => {
		currentYear = new Date().getFullYear();
		years = Array.from({ length: numYears }, (_, i) => currentYear + i);
	});
</script>

<div class="slider-container">
	{#if years.length > 0}
		<input
			type="range"
			min="0"
			max={numYears - 1}
			bind:value={selectedYearIndex}
			class="year-slider"
		/>
		<div class="year-labels">
			{#each years as year, index}
				<span class="year-label" style="left: {(index / (numYears - 1)) * 100}%">
					'{year.toString().slice(-2)}
				</span>
			{/each}
		</div>
	{:else}
		<p>Loading...</p>
	{/if}
</div>

<style>
	.slider-container {
		--input-focus: var(--blue-600);
		--font-color: #323232;
		--font-color-sub: #666;
		--bg-color: #fff;
		--bg-color-alt: #666;
		--main-color: #323232;
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
		padding: 0;
	}
	::selection {
		background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
		color: #000; /* Black text for contrast */
		text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
	}

	.year-slider {
		-webkit-appearance: none;
		width: 100%;
		height: 10px;
		background: var(--blue-500);
		outline: none;
		border: 2px solid var(--main-color);
		border-radius: 5px;
		box-shadow: 2px 2px var(--main-color);
		margin-bottom: 10px;
	}

	.year-slider::-webkit-slider-thumb {
		-webkit-appearance: none;
		appearance: none;
		width: 20px;
		height: 20px;
		background: var(--bg-color);
		cursor: pointer;
		border: 2px solid var(--main-color);
		border-radius: 5px;
		box-shadow: 0 3px 0 var(--main-color);
	}

	.year-slider::-moz-range-thumb {
		width: 25px;
		height: 25px;
		background: var(--bg-color);
		cursor: pointer;
		border: 2px solid var(--main-color);
		border-radius: 5px;
		box-shadow: 0 3px 0 var(--main-color);
	}

	.year-labels {
		position: relative;
		width: 100%;
		height: 20px;
	}

	.year-label {
		position: absolute;
		transform: translateX(-50%);
		font-size: var(--fs-300);
		color: var(--font-color-sub);
	}
</style>
