<script>
  export let bookTitle
  export let bookPrice
  export let bookDescription
  export let buyBook
</script>

<style>
  div {
    margin: 1rem;
    padding: 1rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  }
  h2 {
    font-size: 1rem;
    margin: 0.25rem 0;
    color: aqua;
  }
  p {
    margin: 0.25rem 0;
  }
  button {
    font: larger;
    padding: 0.15rem 0.5rem;
    background-color: #1b1a1a;
    border: 1px solid aliceblue;
    cursor: pointer;
    color: white;
  }
</style>

<div>
  <h2>{bookTitle}</h2>
  <p>{bookPrice}</p>
  <p>{bookDescription}</p>
  <button on:click={buyBook({ title: bookTitle, price: bookPrice })}>
    Buy
  </button>
</div>
