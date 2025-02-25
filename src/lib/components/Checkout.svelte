<script>
	import { onMount } from 'svelte';
	let listaPedidos = 'Carregando...';
	onMount(() => {
		listaPedidos = localStorage.getItem('itemsLista') || 0;
		console.log(listaPedidos);
	});
</script>

<h1>tela checkout</h1>
<p>{listaPedidos}</p>
