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
		<div class="section__header">
			<h1>Svelte/SvelteKit Components</h1>
			<p>These are custom Svelte components.</p>
			<p>(more coming soon!)</p>
		</div>
	</div>
</section>
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
		<p>This is not a true select, but a custom svelte component that acts like a select.</p>
		<Select id="sport" items={sports} />
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

	.section__wrapper p {
		font-size: 0.8rem;
		font-weight: 400;
		padding-block-end: 0.5rem;
	}

	.section__header h1 {
		font-size: 2rem;
		font-weight: 700;
		text-align: center;
	}

	.section__header p {
		font-size: 1rem;
		font-weight: 400;
		padding-block: 0;
		text-align: center;
	}
</style>
