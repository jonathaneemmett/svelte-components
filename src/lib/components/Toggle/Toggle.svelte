<script>
	export let label = 'Toggle Navbar';
	export let checked = false;
	export let style = '';
</script>

<label {style}>
	<input type="checkbox" bind:checked />
	<div class="toggle" />
	{label}
</label>

<style>
	label {
		--width: 40px;
		--height: calc(var(--width) / 2);
		--radius: calc(var(--height) / 2);
		display: flex;
		align-items: center;
		margin-block: 1rem;
		margin-inline: 0.5rem;
	}

	.toggle {
		position: relative;
		width: var(--width);
		height: var(--height);
		border-radius: var(--radius);
		border: 1px solid #333;
		transition: background-color 0.3s ease;
		margin-right: 1rem;
		background-color: var(--toggleBGColor, white);
	}

	.toggle::after {
		content: '';
		position: absolute;
		top: -1px;
		left: 0;
		height: var(--height);
		width: var(--height);
		border-radius: var(--radius);
		background-color: var(--toggleButtonColor, #151515);
		box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.3);
		transition: transform 0.3s ease;
	}

	input {
		display: none;
	}

	input:checked + .toggle {
		background-color: var(--toggle-bg, white);
	}

	input:checked + .toggle::after {
		background-color: teal;
		transform: translate3d(100%, 0, 0);
	}
</style>
