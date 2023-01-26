<script>
	import { fade } from 'svelte/transition';
	import { onMount } from 'svelte';
	/**
	 * @type {any[]}
	 */
	export let items = [];
	export let id = '';
	export let placeholder = 'Select...';
	export let selected = { label: placeholder, value: '' };

	let isOpen = false;
	let chevron__down = false;

	$: isOpen, (chevron__down = !isOpen);

	/**
	 * @param {{ label: string; value: string; }} item
	 */
	function handleSelectChange(item) {
		selected = item;
		isOpen = false;
	}

	/**
	 * @param {any} e
	 */
	function clickedOutside(e) {
		const select = document.querySelector('.select');
		if (!select?.contains(e.target)) {
			isOpen = false;
		}
	}

	onMount(() => {
		document.addEventListener('click', (e) => clickedOutside(e));
		return () => {
			document.removeEventListener('click', clickedOutside);
		};
	});
</script>

<div class="select">
	<!-- So formData has a value -->
	<input type="text" bind:value={selected['label']} {id} hidden />
	<div
		class="select__label"
		on:click={() => (isOpen = !isOpen)}
		on:keydown={() => (isOpen = !isOpen)}
	>
		{#if selected}
			{selected?.label}
		{/if}

		<span class="chevron" class:chevron__down />
	</div>
	<div class="select__menu" class:isOpen in:fade={{ duration: 200 }}>
		{#each items as item}
			<div
				class="select__item"
				on:click={() => handleSelectChange(item)}
				on:keyup={() => handleSelectChange(item)}
			>
				{item.label}
			</div>
		{/each}
	</div>
</div>

<style>
	.select {
		width: 100%;
		position: relative;
		border: 2px solid #e5e5e5;
		border-radius: 0.5rem;
	}

	.select__menu.isOpen {
		opacity: 1;
		visibility: visible;
	}

	.select__label {
		padding: 1rem;
		border-radius: 0.25rem;
		background-color: white;
		display: flex;
		align-items: center;
		justify-content: space-between;
		font-size: 1.2rem;
		cursor: pointer;
	}

	.select__menu {
		border-radius: 0.25rem;
		background-color: white;
		position: absolute;
		top: 105%;
		left: 0;
		right: 0;
		opacity: 0;
		visibility: hidden;
		transition: opacity 0.2s linear, visibility 0.2s linear;
		z-index: 1;
		border: 1px solid #e5e5e5;
	}

	/** Chevron **/
	.chevron {
		border-style: solid;
		border-width: 0.15rem 0.15rem 0 0;
		content: '';
		display: inline-block;
		height: 0.75rem;
		left: 0.15rem;
		position: relative;
		transform: rotate(-45deg);
		width: 0.75rem;
		transition: transform 0.3s linear;
	}

	.chevron.chevron__down {
		transform: rotate(135deg);
	}

	.select__item {
		padding: 1rem;
		font-size: 1.4rem;
	}

	.select__item:hover {
		background-color: #f5f5f5;
		cursor: pointer;
	}
</style>
