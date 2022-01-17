<script lang="ts">
	import { data } from "./data";
	import type { Destination } from "./data";
	import WebPicture from "../../lib/components/WebPicture.svelte";

	let activeDestination: Destination = "moon";
	$: activeData = data.get(activeDestination);

	const switchDestination = (newDestination: Destination) => {
		activeDestination = newDestination;
	};
</script>

<main>
	<div class="content">
		<h1><span>01</span> Pick your destination</h1>
		<div class="layout">
			<div class="img-container layout-left">
				<WebPicture
					webpSrc={data.get(activeDestination).images.webp}
					fallbackSrc={data.get(activeDestination).images.png}
				/>
			</div>
			<div class="layout-right">
				<ul class="destination-picker">
					{#each [...data.keys()] as destination}
						<li>
							<button
								on:click={() => switchDestination(destination)}
								class:active={destination === activeDestination}
								>{destination}</button
							>
						</li>
					{/each}
				</ul>
				<h2>{activeData.name}</h2>
				<p class="description">{activeData.description}</p>
				<div class="info-container">
					<div class="info">
						<h3 class="info-title">Avg. Distance</h3>
						<p>{activeData.distance}</p>
					</div>
					<div class="info">
						<h3 class="info-title">Est. travel time</h3>
						<p>{activeData.travel}</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</main>

<style lang="scss">
	@use "src/styles/_abstracts" as *;
	$media-md: "min-width: 48em";
	$media-lg: "min-width: 72em";

	main {
		@include util--background-image(destination);

		text-align: center;

		@media ($media-lg) {
			text-align: left;
		}
	}

	.content {
		margin-top: 3rem;
		padding: 0 1.5rem 3.625rem;

		@media ($media-lg) {
			padding: 0 $layout--site-padding;
		}
	}

	h1 {
		@include type--heading-5;

		span {
			opacity: 0.25;
		}

		@media ($media-md) {
			text-align: left;

			// align with logo
			padding-left: 1rem;
		}

		// use media query from $lib/components/MainHeader.svelte to align with icon in header
		@media (min-width: 64em) {
			padding-left: 2.15625rem;
		}
		// reset at larget screensize
		@media ($media-lg) {
			padding-left: 0;
		}
	}

	.layout {
		@media ($media-lg) {
			display: flex;
			margin-top: 4rem;
		}
	}

	.layout-right {
		@media ($media-lg) {
			max-width: 27.8125rem;
			margin-left: 9.8125rem;
		}
	}

	.img-container {
		max-width: 10.625rem;
		max-width: clamp(10.625rem, 4.57rem + 25.82vw, 27.81rem);
		margin: 2rem auto 1.625rem;
	}

	.destination-picker {
		width: 14.84375rem;
		width: clamp(14.84375rem, 11.98rem + 12.21vw, 17.84rem);
		min-height: 1.75rem;
		margin: 0 auto;
		@media ($media-lg) {
			margin: 0;
		}

		display: flex;
		justify-content: space-between;

		@include type--nav-2;
		color: $clr--accent-light;
		list-style: none;

		button {
			&.active {
				color: $clr--primary-light;
				pointer-events: none;
			}

			display: flex;
			align-items: flex-start;
			height: 100%;
			line-height: 1;
			position: relative;
			&::after {
				content: "";
				position: absolute;
				bottom: 0;
				left: 0;
				right: 0;
				height: 0.1875rem;
				background-color: $clr--primary-light;

				transition: opacity 0.2s ease-in;

				opacity: 0;
			}

			&:hover::after,
			&:focus::after {
				opacity: 0.5;
			}

			&.active::after {
				opacity: 1;
			}
		}
	}

	h2 {
		@include type--heading-2;
		margin-top: 1.25rem;
	}

	.description {
		max-width: 35.8125rem;
		margin: 0 auto;

		@include type--body;
		color: $clr--accent-light;

		padding-bottom: 2rem;
		border-bottom: 0.0625rem solid #383b4b;
	}

	.info-container {
		@include type--subheading-1;
		display: flex;
		flex-wrap: wrap;
		column-gap: 6.25rem;
		justify-content: center;

		@media ($media-lg) {
			justify-content: flex-start;
		}
	}

	.info {
		margin-top: 2rem;
	}

	.info-title {
		@include type--subheading-2;
		color: $clr--accent-light;
		margin-bottom: 0.75rem;
	}
</style>
