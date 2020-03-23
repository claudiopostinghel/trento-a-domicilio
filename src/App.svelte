<script>

	console.log();

	import Gsheet2Table from './Gsheet2Table.svelte'
	import LINK from './config.js'
	
</script>

<main>
	<h1>Trento a Domicilio</h1>
	
	<Gsheet2Table {LINK} />
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>