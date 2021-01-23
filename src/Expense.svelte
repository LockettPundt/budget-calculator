<script>
  import { getContext } from 'svelte';
  export let name;
  export let id;
  export let cost;
  export let index;
  const { remove, setModifiedExpense } = getContext('state');
  let displayAmount = false;
</script>

<article>
  <div>
    <h2>
      {index}.
      {name}
      <button on:click|once={() => (displayAmount = !displayAmount)}> more </button>
    </h2>
    {#if displayAmount}
      <h4>amount: ${cost}</h4>
    {/if}
  </div>
  <div>
    <button on:click={() => setModifiedExpense(id)}> edit </button>
    <button on:click={() => remove(id)}> delete </button>
  </div>
</article>

<style>
  article {
    margin: 10px 0;
    background-color: cadetblue;
    padding: 10px;
  }
</style>
