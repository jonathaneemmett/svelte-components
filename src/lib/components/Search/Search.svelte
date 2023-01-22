<script>
	import { onMount } from 'svelte';

	let search = '';
	let isEmpty = true;
	let selected = {};

	/**
	 * @type {string | any[]}
	 */
	let items = [];

	/**
	 * @type {string | number | NodeJS.Timeout | undefined}
	 */
	let handler;

	/** @type {string} */
	let debouncedSearch;
	$: search, debounce(search, 500);
	$: debouncedSearch, fetchData();

	$: isEmpty = !items.length;

	/**
	 * @desc    Debounces a value
	 * @param   {string} value
	 * @param   {number} delay
	 */
	function debounce(value, delay) {
		if (!value) return;

		clearTimeout(handler);
		handler = setTimeout(() => {
			debouncedSearch = value;
		}, delay);
	}

	async function fetchData() {
		if (!debouncedSearch) return;

		const response = await fetch(
			`https://ws-public.interpol.int/notices/v1/red?forename=${debouncedSearch}&resultPerPage=100`
		);
		const data = await response.json();

		items = [...data?._embedded?.notices];
	}

	/**
	 * @param {{}} item
	 */
	function handleSearchSelect(item) {
		selected = item;
		reset();
	}

	/**
	 * @param {any} e
	 */
	function clickedOutside(e) {
		if (!e.target.closest('.search__wrapper')) {
			reset();
		}
	}

	function reset() {
		items = [];
		search = '';
		debouncedSearch = '';
	}

	onMount(() => {
		document.addEventListener('click', clickedOutside);
		return () => {
			document.removeEventListener('click', clickedOutside);
		};
	});
</script>

<div class="search__wrapper">
	<input bind:value={search} placeholder="Search" />
	{#if selected && selected?.forename}
		<div class="search__selected">
			{selected?.forename}
			{selected?.date_of_birth}
		</div>
	{/if}
	<ul class="search__results" class:isEmpty>
		{#each items as item}
			{#if item?.forename}
				<li on:click={() => handleSearchSelect(item)} on:keyup={() => handleSearchSelect(item)}>
					{item?.forename}
					{item?.date_of_birth}
				</li>
			{/if}
		{/each}
	</ul>
</div>

<style>
	input {
		width: 100%;
		padding: 1rem;
		border: 1px solid #ccc;
		border-radius: 0.25rem;
		font-size: 1rem;
	}

	ul {
		list-style-type: none;
		margin-inline: 0;
		padding-inline: 1rem;
	}

	li {
		padding-block: 0.5rem;
		padding-inline: 0;
	}

	.search__wrapper {
		position: relative;
	}

	.search__results {
		position: absolute;
		top: 110%;
		left: 0;
		width: 100%;
		background-color: #fff;
		border: 1px solid #ccc;
		border-radius: 0.25rem;
		z-index: 1;
	}

	.search__results.isEmpty {
		display: none;
	}
</style>
