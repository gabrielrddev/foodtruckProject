<script>
	import { onMount } from 'svelte';
	let itemDetails = 'Carregando...';
	onMount(() => {
		itemDetails = localStorage.getItem('item') || 0;
		console.log(itemDetails);
	});
</script>

<h1>pagina gerada automatica</h1>

<h1>tela checkout</h1>
<p>{itemDetails}</p>
