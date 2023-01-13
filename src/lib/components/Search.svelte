<script>
	/** @type {string} */
	let search = '';

	/** @type {object[]} */
	let items = [];

	/**
	 * @type {string | number | NodeJS.Timeout | undefined}
	 */
	let handler;

	/** @type {any} */
	let debouncedSearch;
	$: search, debounce(search, 500);
	$: debouncedSearch, fetchData();

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
		console.log('fetching data...');
		const response = await fetch(
			`https://ws-public.interpol.int/notices/v1/red?forename=${debouncedSearch}&resultPerPage=100`
		);
		const data = await response.json();
		items = [...data?._embedded?.notices];
	}
</script>

<div class="search__wrapper">
	<input bind:value={search} placeholder="Search" />
	<ul>
		{#each items as item}
			<li>{item?.forename} {item?.date_of_birth}</li>
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
</style>
