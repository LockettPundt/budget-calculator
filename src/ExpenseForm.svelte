<script>
  import Title from './Title.svelte';
  let name = '';
  let cost = 0;

  $: empty = !name || !cost;
</script>

<style>
  div {
    width: 20%;
    display: grid;
    grid-template-columns: 1fr;
  }
  p {
    color: red;
  }
</style>

<section>
  <Title title="Add Expense" />
  <form>
    <button>Close</button>
    <div>
      <label for="name">Name</label>
      <input type="text" id="name" bind:value={name} />
      <label for="cost">Cost</label>
      <input type="number" id="cost" bind:value={cost} />
    </div>
    {#if empty}
      <p>please fill out all fields</p>
    {/if}
    <button disabled={empty} type="submit" on:submit={() => console.log(name, cost)}>Submit</button>
  </form>
</section>
