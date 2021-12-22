<script>
  import Item from "./Item.svelte";

  let products = [];
  fetch("https://fritz-kola-challenge.s3-eu-west-1.amazonaws.com/products.json")
    .then(response => response.json())
    .then(data => {
      products = data.products;
    });

  let totalPrice = 0;

  const addItem = function(e) {
    totalPrice += Number(parseFloat(e.detail.price).toFixed(2));
  };
  const removeItem = function(e) {
    totalPrice -= Number(parseFloat(e.detail.price).toFixed(2));
  };
</script>

<style>
  main {
    display:flex;
    flex-direction:column;
  }

  .container{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }

  .row {
    display: flex;
    flex-direction: row;
    text-align: center;
    justify-content: flex-end;
    margin-right:250px;
  }
  h1{
    margin-left:10px;
  }
  .checkout{
    background:purple;
    color:white;
    font-size:16px;
    border:none;
    padding:16px;
    border-radius:10px;
  }

  .totalPrice{
    padding-right:150px;
  }
</style>

<main>
  <div class="container">
    {#each products as product}
      <Item {product} on:addItem={addItem} on:removeItem={removeItem} />
    {/each}
  </div>

  <div class="row totalPrice">
    <h1>Total</h1>

    <h1>{totalPrice}</h1>
  </div>
  <div class="row">
    <button class="checkout">Checkout Button</button>
  </div>
</main>
