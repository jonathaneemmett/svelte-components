<script>
	import Search from '$lib/components/Search.svelte';
	let search = '';
</script>

<section class="search">
	<div class="search__wrapper">
		<Search {search} />
	</div>
</section>

<style>
	.search {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.search__wrapper {
		position: relative;
		width: 100%;
		max-width: 30rem;
	}
</style>
