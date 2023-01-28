<script>
	import '../styles/global.css';
	import SidebarNav from '$lib/components/Navbar/SidebarNav.svelte';

	let toggle = false;

	function toggleSidebar() {
		toggle = !toggle;
	}
</script>

<SidebarNav />
<slot />
