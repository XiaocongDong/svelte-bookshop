<script>
  import BookCard from "./BookCard.svelte";

  let title = "";
  let price = 0;
  let description = "";

  let books = [];
  let booksInCart = [];

  $: booksNumInCart = booksInCart.length;
  $: totalCheckoutPrice = booksInCart.reduce(
    (sum, book) => sum + book.price,
    0
  );

  function handleAddBook() {
    books = books.concat({ title, price, description });
    title = "";
    price = 0;
    description = "";
  }

  function handleAddToCart(title) {
    let bookNeededToBeAdded = books.find(book => book.title == title);
    booksInCart = booksInCart.concat(bookNeededToBeAdded);
  }
</script>

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

  button {
    background-color: #ff3e00;
    color: white;
    border-radius: 5px;
    cursor: pointer;
    border: none;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <h1>Welcome to my online bookstore!</h1>
  <section>
    <h2>Add new book</h2>
    <label for="title">Title</label>
    <input type="text" id="title" bind:value={title} />
    <label for="price">Price</label>
    <input type="number" id="price" bind:value={price} />
    <label for="description">Description</label>
    <textarea rows="3" id="description" bind:value={description} />
    <div>
      <button on:click={handleAddBook}>add book</button>
    </div>
  </section>
  <section>
    <h2>购物车</h2>
    <div>书本总数：{booksNumInCart}</div>
    <div>订单金额：{totalCheckoutPrice}</div>
    {#if booksInCart.length === 0}
      <p>购物车空的哦~</p>
    {:else}
      {#each booksInCart as { title, price }}
        <div>名称: {title}, 价钱: {price}</div>
      {/each}
    {/if}
  </section>
  <section>
    <h2>书单</h2>
    {#each books as { title, price, description }}
      <BookCard {title} {price} {description} {handleAddToCart} />
    {/each}
  </section>
</main>
