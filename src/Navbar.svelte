<script>
  import { getContext } from 'svelte';
  const { showForm } = getContext('state');
</script>

<style>
  div {
    display: grid;
    background-color: aqua;
    grid-template-columns: 1fr 50px;
  }
</style>

<nav>
  <div>
    <h1>Budget Calculator</h1>
    <button type="button" on:click={showForm}> +</button>
  </div>
</nav>
