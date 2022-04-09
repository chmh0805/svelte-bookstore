<script>
  import Book from './book.svelte'
  import Button from './button.svelte'
  import Cart from './cart.svelte'
  let title = ''
  let price = 0
  let description = ''
  let books = []
  let purchases = []
  let totalPrice = 0
  function setTitle(event) {
    title = event.target.value
  }
  function setTotalPrice(value) {
    totalPrice = value
  }
  function addBook() {
    const newBook = {
      title: title,
      price: price,
      description: description,
    }
    books = books.concat(newBook)
  }
  function buyBook(purchase) {
    for (var i = 0; i < books.length; i++) {
      if (
        books[i].title === purchase.title &&
        books[i].price === purchase.price
      ) {
        books.splice(i, 1)
        books = books
        purchases = purchases.concat(purchase)
        totalPrice = 0
        for (let purchase of purchases) {
          totalPrice += purchase.price
        }
        setTotalPrice(totalPrice)
      }
    }
  }
</script>

<style>
  h1 {
    color: purple;
  }
  .cart-div {
    margin: 1rem;
    padding: 1rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    border-bottom: 1px dotted black;
  }
  section {
    margin: auto;
    width: 30rem;
  }
  hr {
    border: 1px solid purple;
  }
  label,
  input,
  textarea {
    width: 100%;
  }
</style>

<section>
  <h1>Add New Book</h1>
  <hr />
  <h2>Add New Book</h2>
  <div>
    <label for="title">Title</label>
    <input type="text" id="title" bind:value={title} on:input={setTitle} />
  </div>
  <div>
    <label for="price">Price</label>
    <input type="number" id="price" bind:value={price} />
  </div>
  <div>
    <label for="description">Description</label>
    <textarea rows="3" id="description" bind:value={description} />
  </div>
  <Button on:click={addBook}>ADD Book</Button>
  <hr />
  <h2>Stock</h2>
  {#if books.length === 0}
    <p>No books in stock.</p>
  {:else}
    {#each books as book}
      <Book
        bookTitle={book.title}
        bookPrice={book.price}
        bookDescription={book.description}
        {buyBook} />
    {/each}
  {/if}
  <hr />
  <h2>Cart</h2>
  {#if purchases.length === 0}
    <p>No books in Cart.</p>
  {:else}
    <div class="cart-div">
      {#each purchases as purchase}
        <Cart title={purchase.title} price={purchase.price} />
      {/each}
    </div>
    <span>Total Price: {totalPrice}</span>
  {/if}
</section>
