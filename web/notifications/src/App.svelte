<script>
	import Kinto from './Kinto.svelte';
	// export let name;
</script>

<main>
	<Kinto></Kinto>
	<slot></slot>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>