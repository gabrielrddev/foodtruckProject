<script>
	import cardapio from '$lib/mock/cardapio.json';
	import Header from './Header.svelte';
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

<div class="min-h-screen bg-gray-50">
	<Header />

	<!-- Navegação de categorias -->
	<div class="mt-4 mb-6 px-4">
		<nav>
			<div class="grid grid-cols-4 gap-2">
				<button
					class="rounded-lg bg-amber-500 px-2 py-2 font-medium text-white shadow-md transition-colors duration-200 hover:bg-amber-600 focus:ring-2 focus:ring-amber-400 focus:outline-none"
					on:click={() => (option = 'entrada')}
				>
					Entradas
				</button>
				<button
					class="rounded-lg bg-amber-500 px-2 py-2 font-medium text-white shadow-md transition-colors duration-200 hover:bg-amber-600 focus:ring-2 focus:ring-amber-400 focus:outline-none"
					on:click={() => (option = 'lanches')}
				>
					Lanches
				</button>
				<button
					class="rounded-lg bg-amber-500 px-2 py-2 font-medium text-white shadow-md transition-colors duration-200 hover:bg-amber-600 focus:ring-2 focus:ring-amber-400 focus:outline-none"
					on:click={() => (option = 'bebidas')}
				>
					Bebidas
				</button>
				<button
					class="rounded-lg bg-amber-500 px-2 py-2 font-medium text-white shadow-md transition-colors duration-200 hover:bg-amber-600 focus:ring-2 focus:ring-amber-400 focus:outline-none"
					on:click={() => (option = 'sobremesa')}
				>
					Sobremesas
				</button>
			</div>
		</nav>
	</div>

	<!-- Lista de itens -->
	<div class="px-4 pb-20">
		{#if getItems(option).length === 0}
			<div class="mt-10 flex items-center justify-center text-gray-500">
				<p>Selecione uma categoria para visualizar os itens</p>
			</div>
		{:else}
			<div class="grid gap-4">
				{#each getItems(option) as item}
					<div class="flex items-center justify-between rounded-lg bg-white p-4 shadow-md">
						<button
							class="flex-grow text-left font-medium text-gray-800 transition-colors duration-200 hover:text-amber-500 focus:outline-none"
							on:click={() => getInfoPage(item)}
						>
							{item.name}
						</button>
						<div class="flex items-center gap-3">
							<span class="font-bold text-gray-700">R$ {item.price}</span>
							<button
								class="flex h-8 w-8 items-center justify-center rounded-full bg-green-500 text-white shadow-md transition-colors duration-200 hover:bg-green-600 focus:ring-2 focus:ring-green-400 focus:outline-none"
								on:click={() => addCart(item)}
							>
								+
							</button>
						</div>
					</div>
				{/each}
			</div>
		{/if}
	</div>

	<!-- Botão de carrinho fixo -->
	<div class="fixed right-0 bottom-4 left-0 flex justify-center">
		<button
			class="flex items-center gap-2 rounded-full bg-amber-600 px-6 py-3 font-bold text-white shadow-lg transition-colors duration-200 hover:bg-amber-700 focus:ring-2 focus:ring-amber-400 focus:outline-none"
			on:click={saveCheckout}
		>
			<svg
				xmlns="http://www.w3.org/2000/svg"
				class="h-5 w-5"
				viewBox="0 0 20 20"
				fill="currentColor"
			>
				<path
					d="M3 1a1 1 0 000 2h1.22l.305 1.222a.997.997 0 00.01.042l1.358 5.43-.893.892C3.74 11.846 4.632 14 6.414 14H15a1 1 0 000-2H6.414l1-1H14a1 1 0 00.894-.553l3-6A1 1 0 0017 3H6.28l-.31-1.243A1 1 0 005 1H3z"
				/>
			</svg>
			Carrinho {carrinho.length > 0 ? `(${carrinho.length})` : ''}
		</button>
	</div>
</div>
