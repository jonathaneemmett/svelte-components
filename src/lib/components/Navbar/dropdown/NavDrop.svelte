<script>
	import Fa from 'svelte-fa';
	import { faFire } from '@fortawesome/free-solid-svg-icons';
	export let title = '';

	let isOpen = false;
	let chevron__down = false;

	$: isOpen, (chevron__down = isOpen);
</script>

<button class="dropdown__btn" on:click={() => (isOpen = !isOpen)}>
	<Fa icon={faFire} />
	<span class="dropdown__title">{title}</span>
	<span class="chevron right" class:chevron__down />
</button>

<div class="dropdown__container" class:isOpen>
	<a href="">Test</a>
	<a href="">Test</a>
	<a href="">Test</a>
	<a href="">Test</a>
	<a href="">Test</a>
	<a href="">Test</a>
	<a href="">Test</a>
</div>

<style>
	.dropdown__btn {
		display: flex;
		justify-content: flex-start;
		list-style: none;
		height: 60px;
		padding: 1rem;
		color: #f5f5f5;
		text-decoration: none;
		border: none;
		background: none;
		font-size: 1.2rem;
		display: flex;
		align-items: center;
		transition: 0.3s;
		gap: 1rem;
		width: 100%;
	}

	/* On mouse-over */
	.dropdown__btn:hover {
		color: #f1f1f1;
	}

	.dropdown__container {
		display: none;
		opacity: 0;
		visibility: hidden;
		transition: opacity 3s linear, visibility 3s linear;
	}

	.dropdown__container.isOpen {
		display: block;
		opacity: 1;
		visibility: visible;
	}

	.dropdown__container a {
		color: #f5f5f5;
		padding: 12px 16px;
		text-decoration: none;
		display: block;
		transition: 0.3s;
	}

	/** Chevron **/
	.chevron {
		border-style: solid;
		border-width: 0.15rem 0.15rem 0 0;
		content: '';
		display: inline-block;
		height: 0.5rem;
		width: 0.5rem;
		left: 0rem;
		position: relative;
		transform: rotate(45deg);
		transition: transform 0.3s linear;
	}

	.chevron.chevron__down {
		transform: rotate(135deg);
	}
</style>
