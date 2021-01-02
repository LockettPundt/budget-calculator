<script>
  import Navbar from './Navbar.svelte';
  import ExpenseList from './ExpenseList.svelte';
  import expensivesData from './expensives';
  let expensives = [...expensivesData];

  console.log(expensives);
</script>

<style>
  :global(body) {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
  }
</style>

<div class="App">
  <Navbar />
  <ExpenseList expenses={expensives} />
</div>
