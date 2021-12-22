<script>
  import { createEventDispatcher } from "svelte";

  export let product;

  const dispatch = createEventDispatcher();
  const price = Number(parseFloat(product.price).toFixed(2));
  const productImageStyle = 'background-image: url("' + product.image + '");';

  let quantity = 0;

  let removeItem = function() {
    if (quantity > 0) {
      dispatch("removeItem", {
        price: price
      });
      quantity -= 1;
    }
  };

  let addItem = function() {
    quantity += 1;
    dispatch("addItem", {
      price: price
    });
  };
</script>

<style>
  main {
    display: flex;
    flex-direction: column;
    max-width: fit-content;
    font-size: 16px;
    margin:20px;
  }

  .row {
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .topRow {
    min-height: 200px;
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
    margin-bottom: 20px;
  }

  button {
    background-color: purple;
    margin-left: 5px;
    margin-right: 5px;
    border: none;
    border-radius: 5px;
    padding-left: 15px;
    padding-right: 15px;
    padding-top: 10px;
    padding-bottom: 10px;
    color: white;
  }

  .quantitySpan {
    margin-right: 20px;
  }
  .numberSpan {
    margin-right: 20px;
  }

  .priceTag {
      background:grey;
      padding:5px;
      align-self:flex-end;
      justify-self:flex-end;
      margin-left:auto;
  }
</style>

<main>
  <div class="row topRow" style={productImageStyle}>
    <span class="priceTag">{product.price}</span>

  </div>
  <div class="row">
    <span class="quantitySpan">Quantity :</span>
    <span class="numberSpan">{quantity}</span>

    <button on:click={addItem}>+</button>
    <button on:click={removeItem}>-</button>

  </div>

</main>
