<script>
	import cardapio from '$lib/mock/cardapio.json';
	import { goto } from '$app/navigation';

	let carrinho = [];
	let option = '';

	function getItems(option) {
		switch (option) {
			case 'entrada':
				return cardapio.entradas;
			case 'lanches':
				return cardapio.lanches;
			case 'bebidas':
				return cardapio.bebidas;
			case 'sobremesa':
				return cardapio.sobremesa;
			default:
				return [];
		}
	}
	function addCart(item) {
		carrinho = [...carrinho, item];
		console.log(carrinho);
		localStorage.setItem('itemsLista', JSON.stringify(carrinho));
		return JSON.stringify(carrinho);
	}
	function saveCheckout() {
		goto('/checkout');
	}
	function getInfoPage(item) {
		let itemDetails = item.name;
		localStorage.setItem('item', itemDetails);
		goto('/generationPage');
	}
</script>

<nav>
	<div>Cardápio Digital</div>
	<div class="flex justify-center">
		<button on:click={() => (option = 'entrada')}> Entradas </button>
		<button on:click={() => (option = 'lanches')}> Lanches </button>
		<button on:click={() => (option = 'bebidas')}> Bebidas </button>
		<button on:click={() => (option = 'sobremesa')}> Sobremesas </button>
	</div>
	<button on:click={saveCheckout}>Carrinho</button>
</nav>

{#each getItems(option) as item}
	<div class="">
		<button on:click={() => getInfoPage(item)}>{item.name}</button>
		{item.price} <button on:click={() => addCart(item)}>+</button>
	</div>
{/each}
