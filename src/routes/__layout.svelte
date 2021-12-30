<script lang="ts">
	import { page } from "$app/stores";

	import "../styles/global.scss";
	import logoIcon from "/icons/logo.svg";

	const navTargets = [
		{ label: "Home", url: "/" },
		{ label: "Destination", url: "/destination" },
		{ label: "Crew", url: "/crew" },
		{ label: "Technology", url: "/technology" }
	];
</script>

<header>
	<div class="logo">
		<a href="/"><img src={logoIcon} alt="" /></a>
	</div>
	<nav>
		<ol>
			{#each navTargets as target}
				<li>
					<a class:active={target.url === $page.path} href={target.url}
						>{target.label}</a
					>
				</li>
			{/each}
		</ol>
	</nav>
</header>
<slot />

<style lang="scss">
	@use "src/styles/_abstracts" as *;

	header {
		position: absolute;
		top: 2.5rem;
		width: 100vw;
		display: flex;
		justify-content: space-between;
		align-items: center;
		// padding-left: $site-padding;
	}

	.logo {
		width: $site-padding;

		img {
			display: block;
			margin: 0 auto;
		}
	}

	nav {
		@include type-nav;

		width: 100%;
		// margin-left: 4rem;

		position: relative;

		&::before {
			content: "";
			background-color: white;
			opacity: 0.25;
			height: 0.2rem;
			display: block;
			position: absolute;
			top: 50%;
			left: 0;
			right: 50rem;

			z-index: 1;
		}
	}

	ol {
		height: 6rem;
		padding-right: $site-padding;
		padding-left: 7.6875rem;
		width: fit-content;
		margin-left: auto;

		background: rgba(255, 255, 255, 0.04);
		backdrop-filter: blur(81.5485px);

		display: flex;
		justify-content: flex-end;
		align-items: center;
		gap: 3rem;

		counter-reset: list -1;
		list-style-type: none;
	}

	li {
		height: 100%;
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;

		counter-increment: list;
		text-transform: uppercase;

		&.active {
			pointer-events: none;
		}

		&::before {
			content: "0" counter(list);
			font-weight: 700;

			padding-right: 0.625rem;
		}

		position: relative;

		&::after {
			content: "";
			position: absolute;
			bottom: 0;
			height: 0.1875rem;
			width: 100%;

			background-color: $clr-primary-light;

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
