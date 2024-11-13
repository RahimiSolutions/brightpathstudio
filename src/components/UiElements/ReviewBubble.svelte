<script>
	let { imageSrc = '', review = '' } = $props();

	let isHovered = $state(false);
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<div
	class="review-card"
	onmouseenter={() => (isHovered = true)}
	onmouseleave={() => (isHovered = false)}
>
	<!-- Circular Image -->
	<div class="profile-image">
		<img src={imageSrc} alt="Reviewer" />
	</div>

	<!-- Expandable Notification Badge -->
	<div class="notification-badge" class:expanded={isHovered}>
		<p class="review-text">{review}</p>
	</div>
</div>

<style lang="scss">
	::selection {
		background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
		color: #000; /* Black text for contrast */
		text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
	}
	.review-card {
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 120px;
		height: 120px;
	}

	.profile-image {
		position: relative;
		width: 120px;
		height: 120px;
		border-radius: 50%;
		overflow: hidden;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.profile-image img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 50%;
		transition: transform 0.3s ease-in-out;
	}

	/* Notification Badge */
	.notification-badge {
		position: absolute;
		top: 5px;
		right: 5px;
		width: 20px;
		height: 20px;
		background-color: var(--blue-600);
		border-radius: 12px;
		border: 2px solid white;
		cursor: pointer;
		transition: all 0.5s cubic-bezier(0.68, -0.55, 0.27, 1.55);
		overflow: hidden;
		display: flex;
		align-items: center;
		justify-content: flex-start;
		padding: 0;
	}

	.notification-badge.expanded {
		width: 200px;
		height: auto;
		min-height: 50px;
		top: -50px;
		right: -185px;
		padding: 10px;
		backdrop-filter: blur(10px);
		box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
	}

	.review-text {
		opacity: 0;
		transition: opacity 0.3s ease-in-out;
		text-align: left;
		margin: 0;
		width: 100%;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		font-family: 'Sfpro';
		font-size: var(--fs-400);
		color: var(--white);
	}

	.notification-badge.expanded .review-text {
		opacity: 1;
		white-space: normal;
	}
</style>
