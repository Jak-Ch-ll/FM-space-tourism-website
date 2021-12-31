<svelte:head>
	<title>Space Tourism</title>
</svelte:head>

<main>
	<div class="text">
		<h1>
			So, you want to travel to <div>Space</div>
		</h1>
		<p>
			Let’s face it; if you want to go to space, you might as well genuinely go
			to outer space and not hover kind of on the edge of it. Well sit back, and
			relax because we’ll give you a truly out of this world experience!
		</p>
	</div>
	<button>Explore</button>
</main>

<style lang="scss">
	@use "src/styles/_abstracts" as *;

	:global(body) {
		background-image: url("/imgs/home/background-home-desktop.jpg");
	}

	main {
		padding: $site-padding;
		height: 100%;

		display: flex;
		align-items: flex-end;
		justify-content: space-between;
	}

	h1 {
		@include type-heading-5;
	}

	h1 > div {
		@include type-heading-1;

		margin: 1.5rem 0;
	}

	p {
		@include type-body;

		color: $clr-accent-light;
		max-width: 27.75rem;
	}

	button {
		@include type-heading-4;

		$size: 17.125rem;

		color: $clr-primary-dark;
		background-color: $clr-primary-light;
		border-radius: 50%;
		height: $size;
		width: $size;
		text-align: center;

		cursor: pointer;

		position: relative;

		&::after {
			content: "";
			position: absolute;
			background-color: rgba($clr-primary-light, 0.1);
			height: $size + 11rem;
			width: $size + 11rem;
			top: -5.5rem;
			left: -5.5rem;
			border-radius: 50%;
			z-index: -1;

			@media not screen and (prefers-reduced-motion) {
				transform: scale(0.6);
				transition: transform 0.4s ease-in-out;
			}

			@media (prefers-reduced-motion) {
				opacity: 0;
				transition: opacity 0.5s ease-in-out;
			}
		}

		&:hover::after {
			@media not screen and (prefers-reduced-motion) {
				transform: scale(1);
			}

			@media (prefers-reduced-motion) {
				opacity: 1;
			}
		}
	}
</style>
