<script>
	import { onMount } from 'svelte';
	let itemDetails = 'Carregando...';
	onMount(() => {
		itemDetails = localStorage.getItem('item');
		console.log(itemDetails);
	});
</script>

<h1>pagina gerada automatica</h1>

<p>{itemDetails}</p>
