<svelte:head>
	<title>Space Tourism</title>
</svelte:head>

<main>
	<div class="content">
		<div class="text">
			<h1>
				So, you want to travel to <div>Space</div>
			</h1>
			<p>
				Let’s face it; if you want to go to space, you might as well genuinely
				go to outer space and not hover kind of on the edge of it. Well sit
				back, and relax because we’ll give you a truly out of this world
				experience!
			</p>
		</div>
		<a class="cta" href="/destination">Explore</a>
	</div>
</main>

<style lang="scss">
	@use "src/styles/_abstracts" as *;

	main {
		@include util--background-image(home);
	}

	.content {
		height: 100%;

		display: flex;
		justify-content: space-between;

		flex-direction: column;
		align-items: center;
		padding: 1.5rem;
		padding-top: 12.8vh;

		text-align: center;

		@include media--desktop {
			margin-top: 27.9vh;

			padding: 0 $layout--site-padding;
			flex-direction: row;
			align-items: flex-end;

			text-align: left;
		}
	}

	h1 {
		@include type--heading-5;
	}

	h1 > div {
		margin: 1.5rem 0;

		@include type--heading-1;
	}

	p {
		max-width: 27.75rem;

		@include type--body;
		color: $clr--accent-light;
	}

	.cta {
		@include type--heading-4;

		margin-top: clamp(5.06rem, 0.59rem + 19.08vw, 9.75rem);
		@include media--desktop {
			margin-top: 0;
		}

		display: flex;
		justify-content: center;
		align-items: center;

		--size: 9.375rem;
		--size: clamp(9.38rem, 6.78rem + 11.08vw, 16.75rem);

		color: $clr--primary-dark;
		background-color: $clr--primary-light;
		border-radius: 50%;
		height: var(--size);
		width: var(--size);

		cursor: pointer;

		// hover effect
		position: relative;
		z-index: 0;
		&::after {
			content: "";
			position: absolute;
			background-color: rgba($clr--primary-light, 0.1);
			top: 0;
			right: 0;
			bottom: 0;
			left: 0;
			border-radius: 50%;
			z-index: -1;

			transition: transform 0.4s ease-in-out;

			@media (prefers-reduced-motion) {
				transform: scale(1.64);
				opacity: 0;
				transition: opacity 0.5s ease-in-out;
			}
		}

		&:hover::after {
			transform: scale(1.64);
			opacity: 1;
		}
	}
</style>
