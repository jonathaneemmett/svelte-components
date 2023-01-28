<script>
	import '../styles/global.css';
	import Navbar from '$lib/components/Navbar/Navbar.svelte';
	import SidebarNav from '$lib/components/Navbar/SidebarNav.svelte';
	import Toggle from '$lib/components/Toggle/Toggle.svelte';

	let toggle = false;

	function toggleSidebar() {
		toggle = !toggle;
	}
</script>

<!-- {#if !toggle}
	
{:else}
	<Navbar />
{/if}
<Toggle bind:checked={toggle} on:click={toggleSidebar} /> -->
<SidebarNav />
<slot />
