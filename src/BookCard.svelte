<script>
  export let title;
  export let price;
  export let description;
  export let handleAddToCart;
</script>

<style>
  .card {
    text-align: left;
    border-radius: 5px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    padding: 10px;
  }

  h1 {
    font-size: 20px;
  }

  h2 {
    font-size: 15px;
    color: #999;
  }

  button {
    background-color: #ff3e00;
    color: white;
    border-radius: 5px;
    cursor: pointer;
    border: none;
  }
</style>

<div class="card">
  <h1>{title}</h1>
  <h2>${price}</h2>
  <p>{description}</p>
  <button on:click={() => handleAddToCart(title)}>添加到购物车</button>
</div>
