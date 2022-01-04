<script lang="ts">
	import { page } from "$app/stores";

	import logoIcon from "$lib/assets/icons/logo.svg";
	import menuIcon from "$lib/assets/icons/icon-hamburger.svg";
	import menuCloseIcon from "$lib/assets/icons/icon-close.svg";

	const navTargets = [
		{ label: "Home", url: "/" },
		{ label: "Destination", url: "/destination" },
		{ label: "Crew", url: "/crew" },
		{ label: "Technology", url: "/technology" }
	];

	let menuOpen = false;
</script>

<header>
	<div class="logo">
		<a href="/"><img src={logoIcon} alt="Home" /></a>
	</div>
	<button class="toggle-menu-btn" on:click={() => (menuOpen = !menuOpen)}>
		<img
			src={menuOpen ? menuCloseIcon : menuIcon}
			alt={`${menuOpen ? "Close" : "Open"} menu`}
		/>
	</button>
	<nav>
		<ol class:menuOpen>
			{#each navTargets as target}
				<li>
					<a class:active={target.url === $page.url.pathname} href={target.url}
						>{target.label}</a
					>
				</li>
			{/each}
		</ol>
	</nav>
</header>

<style lang="scss">
	@use "src/styles/_abstracts" as *;

	$media-md: "min-width: 44em";
	$media-lg: "min-width: 64em";

	:global(main) {
		padding-top: 4.5rem;

		@media ($media-md) {
			padding-top: 6rem;
		}

		@media ($media-lg) {
			padding-top: 6rem + 1.5rem;
		}
	}

	header {
		position: absolute;
		width: 100%;
		max-width: $layout--site-max-width;

		padding: 1.5rem;
		padding-bottom: 0;
		display: flex;
		justify-content: space-between;
		align-items: center;

		@media ($media-md) {
			padding: 0;
			padding-left: 2.5rem;
		}

		@media ($media-lg) {
			padding: 0;
			padding-top: 2.5rem;
			$margin-left: calc((100vw - $layout--site-max-width) * 0.5);
			margin-left: max(0rem, $margin-left);
		}
	}

	.logo {
		width: $layout--site-padding;
		flex-shrink: 0;

		img {
			display: block;

			@media ($media-lg) {
				margin: 0 auto;
			}
		}
	}

	.toggle-menu-btn {
		z-index: 900;

		@media ($media-md) {
			display: none;
		}
	}

	nav {
		position: absolute;
		top: 0;
		right: 0;
		height: 100vh;
		z-index: 1;

		@include type--nav;

		@media ($media-md) {
			position: relative;
			width: 100%;
			height: auto;
		}

		// decorative line on large displays
		@media ($media-lg) {
			&::before {
				content: "";
				position: absolute;
				display: block;
				top: 50%;
				left: 0;
				right: 50rem;
				height: 0.2rem;

				background-color: $clr--primary-light;
				opacity: 0.25;
				z-index: 100;
			}
		}
	}

	ol {
		height: 100%;
		min-width: 15.875rem;

		padding-left: 2rem;
		padding-top: 7.275rem;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: flex-start;
		& > * + * {
			margin-top: 2rem;
		}

		@mixin blur {
			background-color: rgba($clr--primary-dark, 0.8);

			@supports (backdrop-filter: blur(81.5485px)) {
				background: rgba(255, 255, 255, 0.04);
				backdrop-filter: blur(81.5485px);
			}
		}
		@include blur;

		// preperation for the numbering
		counter-reset: list -1;
		list-style-type: none;

		@media ($media-md) {
			height: 6rem;
			width: fit-content;
			margin-left: auto;

			padding: 0 3rem;
			flex-direction: row;
			justify-content: flex-end;
			align-items: center;
			& > * + * {
				margin-top: 0;
				margin-left: 3rem;
			}
		}

		@media ($media-lg) {
			padding: {
				right: $layout--site-padding;
				left: 7.6875rem;
			}

			// use pseudo element for background und larger screens, because it needs to overflow to the edge of the screen
			background: none;
			backdrop-filter: none;
			position: relative;
			&::after {
				content: "";
				position: absolute;
				top: 0;
				left: 0;
				bottom: 0;
				z-index: -1;

				@include blur;

				// calc negative overflow when site width is smaller then the available space
				$right-overflow: calc((100vw - #{$layout--site-max-width}) * -0.5);
				// only apply negative overflow
				right: min(0rem, $right-overflow);
			}
		}

		// animation: fade; additionally shrink menu to 0, so its not clickable but still accessible via screen readers
		opacity: 0;
		transform: scale(0);
		transition: opacity 0.2s ease-in, transform 0s 0.2s;

		&.menuOpen {
			opacity: 1;
			transform: scale(1);
			transition: opacity 0.2s ease-in;
		}

		@media ($media-md) {
			opacity: 1;
			transform: scale(1);
		}
	}

	li {
		width: 100%;
		@media ($media-md) {
			height: 100%;
		}
	}

	li a {
		display: flex;
		height: 100%;
		align-items: center;

		text-transform: uppercase;
		color: $clr--primary-light;

		counter-increment: list;

		&.active {
			pointer-events: none;
		}

		// numbering
		&::before {
			content: "0" counter(list);
			font-weight: 700;

			padding-right: 0.625rem;

			@media ($media-md) {
				display: none;
			}

			@media ($media-lg) {
				display: inline;
			}
		}

		// hover/active marker
		position: relative;

		&::after {
			content: "";
			position: absolute;
			right: 0;
			width: 0.25rem;
			height: 100%;

			@media ($media-md) {
				bottom: 0;
				height: 0.1875rem;
				width: 100%;
			}

			background-color: $clr--primary-light;

			opacity: 0;
			transition: opacity 0.2s ease-in;
		}

		&.active::after {
			opacity: 1;
		}

		&:hover::after {
			opacity: 0.5;
		}
	}
</style>
