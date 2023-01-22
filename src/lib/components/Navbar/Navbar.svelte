<script>
	import { onMount } from 'svelte';

	let active = false;
	let checked = false;

	onMount(() => {
		let url = window.location.href;

		/** @type {NodeListOf<HTMLAnchorElement>}*/
		let menu = document.querySelectorAll('.menu li a');
		menu.forEach((link) => {
			link.addEventListener('click', () => {
				menu.forEach((link) => {
					link.classList.remove('active');
				});
				link.classList.add('active');
				checked = false;
			});
		});

		menu.forEach((link) => {
			if (link?.href === url) {
				link.classList.add('active');
			}
		});
	});
</script>

<nav class="navbar">
	<div class="logo">LOGO</div>
	<!-- Navigation Menu -->
	<ul class="nav-links">
		<!-- Checkbox Hack -->
		<input type="checkbox" id="checkbox_toggle" bind:checked />
		<label for="checkbox_toggle" class="hamburger">&#9776;</label>

		<!-- Navigation Items -->
		<div class="menu">
			<li><a href="/" class:active>Home</a></li>
			<li><a href="/about" class:active>About</a></li>
			<li><a href="/contact" class:active>Contact</a></li>
		</div>
	</ul>
</nav>

<style>
	.navbar {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding-block: 1rem;
		padding-inline: 1rem;
		background-color: #fff;
		color: #151515;
	}

	.nav-links a {
		color: #151515;
	}

	.logo {
		font-size: 1.5rem;
	}

	.menu {
		display: flex;
		gap: 1em;
		font-size: 1.2rem;
	}

	.menu li:hover {
		width: 100%;
		background-color: #151515;
		transition: 0.3s ease-in-out;
	}

	.menu li {
		padding-block: 0.25rem;
		padding-inline: 0.5rem;
	}

	a.active {
		color: purple;
	}

	/* Responsive */
	input[type='checkbox'] {
		display: none;
	}

	.hamburger {
		display: none;
		font-size: 1.5rem;
		user-select: none;
	}

	/* Media Queries */
	@media (max-width: 62.5em) {
		.menu {
			display: none;
			position: absolute;
			background-color: #ffffff;
			right: 0;
			left: 0;
			text-align: center;
			padding-block: 1rem;
			z-index: 1;
		}

		.menu li:hover {
			display: inline-block;
			background-color: #4c9e9e;
			transition: 0.3s ease-in-out;
			cursor: pointer;
		}

		.menu li + li {
			margin-top: 1rem;
		}

		input[type='checkbox']:checked ~ .menu {
			display: block;
		}

		.hamburger {
			display: block;
		}
	}
</style>
