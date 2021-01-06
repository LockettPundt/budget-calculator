<script>
  import { setContext } from 'svelte';
  import Navbar from './Navbar.svelte';
  import Total from './Total.svelte';
  import ExpenseForm from './ExpenseForm.svelte';
  import ExpenseList from './ExpenseList.svelte';
  import expensivesData from './expensives';
  let expensives = [...expensivesData];

  const state = {
    remove: (id) => (expensives = expensives.filter((item) => item.id !== id)),
    add: () => console.log('adding an item'),
    clear: () => (expensives = []),
  };

  $: total = expensives.reduce((sum, x) => (sum += x.cost), 0);

  setContext('state', state);
</script>

<style>
  :global(body) {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
  }
</style>

<div class="App">
  <Navbar />
  <ExpenseForm />
  <ExpenseList expenses={expensives} />
  <Total title="Total Expenses" {total} />
  <button on:click={() => state.clear()}>Clear List</button>
</div>
