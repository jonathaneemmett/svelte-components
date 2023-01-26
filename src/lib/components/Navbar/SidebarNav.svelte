<script>
	import Fa from 'svelte-fa';
	import {
		faBars,
		faHome,
		faFire,
		faChevronCircleDown,
		faPlayCircle,
		faHistory,
		faClock
	} from '@fortawesome/free-solid-svg-icons';
	import { onMount } from 'svelte';

	let active = false;

	onMount(() => {
		const showMenu = document.getElementById('show-menu');
		const navMenu = document.getElementById('nav-menu');

		showMenu?.addEventListener('click', () => {
			navMenu?.classList.toggle('active');
		});
		return () => {
			showMenu?.removeEventListener('click', () => {
				navMenu?.classList.toggle('active');
			});
		};
	});
</script>

<div id="navbar">
	<a href="#" class="menu__bars" id="show-menu">
		<Fa icon={faBars} />
		<h1>LOGO</h1>
	</a>
</div>
<nav id="nav-menu" class:active>
	<ul class="nav__menu-items">
		<hr />
		<div class="nav__section">
			<li class="nav__text">
				<a href="#">
					<Fa icon={faHome} /> Home
				</a>
			</li>
			<li class="nav__text">
				<a href="#">
					<Fa icon={faFire} /> Trending
				</a>
			</li>
			<li class="nav__text">
				<a href="#">
					<Fa icon={faChevronCircleDown} /> Subscriptions
				</a>
			</li>
		</div>
		<hr />
		<div class="nav__section">
			<li class="nav__text">
				<a href="#">
					<Fa icon={faPlayCircle} /> Library
				</a>
			</li>
			<li class="nav__text">
				<a href="#">
					<Fa icon={faHistory} /> History
				</a>
			</li>
			<li class="nav__text">
				<a href="#">
					<Fa icon={faClock} /> Watch Later
				</a>
			</li>
		</div>
	</ul>
</nav>

<style>
	hr {
		background-color: #464646;
		border: none;
		height: 1px;
	}

	#navbar {
		background-color: #212121;
		height: 100px;
		display: flex;
		justify-content: flex-start;
		align-items: center;
		z-index: 1;
	}

	.menu__bars {
		color: #fff;
		font-size: 2rem;
		margin-inline-start: 2rem;
		padding-block: 1rem;
		cursor: pointer;
		display: flex;
		align-items: center;
		gap: 1rem;
	}

	.menu__bars h1 {
		color: #fff;
		font-size: 1.5rem;
	}

	#nav-menu {
		background-color: #212121;
		width: 250px;
		height: 100vh;
		display: flex;
		justify-content: center;
		position: fixed;
		top: 100px;
		left: -100%;
		transition: 0.3s;
		z-index: 1;
	}

	#nav-menu.active {
		left: 0;
	}

	.nav__text {
		display: flex;
		justify-content: flex-start;
		list-style: none;
		height: 60px;
		padding: 1rem;
	}

	.nav__text a {
		color: #f5f5f5;
		text-decoration: none;
		font-size: 1.2rem;
		display: flex;
		align-items: center;
		transition: 0.3s;
		gap: 1rem;
	}

	.nav__text a:hover {
		background-color: rgba(144, 144, 144, 0.219);
	}

	.nav__menu-items {
		width: 100%;
	}

	.nav__icon {
		padding-inline-end: 1rem;
		color: #909090;
	}

	.nav__section {
		height: 200px;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
</style>
