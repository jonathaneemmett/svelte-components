<script>
	import Select from '$lib/components/Select/Select.svelte';
	import Search from '$lib/components/Search/Search.svelte';

	const sports = [
		{ label: 'Football', value: 'football' },
		{ label: 'Baseball', value: 'baseball' },
		{ label: 'Basketball', value: 'basketball' },
		{ label: 'Hockey', value: 'hockey' }
	];
</script>

<section class="section">
	<div class="section__wrapper">
		<h2 class="section__headline">Search with debounce demo</h2>
		<p>(searches interpol as a demo)</p>
		<Search />
	</div>
</section>
<section class="section">
	<div class="section__wrapper">
		<h2 class="section__headline">Select component demo</h2>
		<Select items={sports} />
	</div>
</section>

<style>
	.section {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding-block: 2rem;
	}

	.section__wrapper {
		position: relative;
		width: 100%;
		max-width: 30rem;
	}
</style>
