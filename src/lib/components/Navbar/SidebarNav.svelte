<script>
	import NavDrop from './dropdown/NavDrop.svelte';
	import Hamburger from './shared/Hamburger.svelte';
	import Fa from 'svelte-fa';
	import {
		faHome,
		faChevronCircleDown,
		faPlayCircle,
		faHistory,
		faClock
	} from '@fortawesome/free-solid-svg-icons';

	let active = false;

	function toggleMenu() {
		active = !active;
	}
</script>

<div id="navbar">
	<a href="#" class="menu__bars" id="show-menu" on:click={toggleMenu}>
		<Hamburger {active} />
		<h1>LOGO</h1>
	</a>
</div>
<nav id="nav-menu" class:active>
	<hr />
	<div class="nav__section">
		<a class="nav__item" href="#">
			<Fa icon={faHome} /> Home
		</a>
		<NavDrop title="Components" />
		<a class="nav__item" href="#">
			<Fa icon={faChevronCircleDown} /> Subscriptions
		</a>
	</div>
	<hr />
	<div class="nav__section">
		<a class="nav__item" href="#">
			<Fa icon={faPlayCircle} /> Library
		</a>
		<a class="nav__item" href="#">
			<Fa icon={faHistory} /> History
		</a>
		<a class="nav__item" href="#">
			<Fa icon={faClock} /> Watch Later
		</a>
	</div>
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
		flex-direction: column;
		align-items: flex-start;
		justify-content: flex-start;
		position: fixed;
		top: 100px;
		left: -100%;
		transition: 0.3s;
		z-index: 1;
	}

	#nav-menu.active {
		left: 0;
	}

	.nav__item {
		display: flex;
		justify-content: flex-start;
		list-style: none;
		height: 60px;
		padding: 1rem;
		color: #f5f5f5;
		text-decoration: none;
		font-size: 1.2rem;
		display: flex;
		align-items: center;
		transition: 0.3s;
		gap: 1rem;
		width: 100%;
	}
	.nav__section {
		display: flex;
		flex-direction: column;
		justify-content: center;
	}

	/* Icon */
</style>
