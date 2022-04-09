<script>
  import Book from './book.svelte'
  import Button from './button.svelte'
  let title = ''
  let price = 0
  let description = ''
  let books = []
  function setTitle(event) {
    title = event.target.value
  }
  function addBook() {
    const newBook = {
      title: title,
      price: price,
      description: description,
    }
    books = books.concat(newBook)
  }
</script>

<style>
  h1 {
    color: purple;
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
      <Book bookTitle={title} bookPrice={price} bookDescription={description} />
    {/each}
  {/if}
</section>
