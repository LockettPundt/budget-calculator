<script>
  import { setContext, onMount, afterUpdate } from 'svelte';
  import Navbar from './Navbar.svelte';
  import Total from './Total.svelte';
  import ExpenseForm from './ExpenseForm.svelte';
  import ExpenseList from './ExpenseList.svelte';
  let expensives = [];

  const state = {
    remove: (id) => (expensives = expensives.filter((item) => item.id !== id)),
    add: (options) => {
      showForm = false;
      expensives = [
        ...expensives,
        {
          ...options,
          id: Math.max(...expensives.map((x) => x.id)) + 1,
        },
      ];
    },
    edit: ({ name, cost }) => {
      showForm = false;
      expensives = expensives.map((item) => {
        if (item.id === setId) {
          return {
            ...item,
            name,
            cost,
          };
        }
        return item;
      });
      setCost = null;
      setId = null;
      setName = '';
    },
    clear: () => (expensives = []),
    setModifiedExpense: (id) => {
      showForm = true;
      let expense = expensives.find((item) => item.id === id);
      setName = expense.name;
      setCost = expense.cost;
      setId = expense.id;
    },
    hideForm: () => {
      showForm = false;
      setName = '';
      setCost = null;
      setId = null;
    },
    showForm: () => (showForm = true),
  };

  function setLocalStorage() {
    localStorage.setItem('expenses', JSON.stringify(expensives));
  }

  let setName = '';
  let setCost = null;
  let setId = null;

  $: showForm = false;
  $: isEditing = !!setId;
  $: total = expensives.reduce((sum, x) => (sum += x.cost), 0);

  setContext('state', state);
  onMount(() => {
    if (localStorage.getItem('expenses')) {
      expensives = JSON.parse(localStorage.getItem('expenses'));
    } else {
      expensives = [];
    }
  });
  afterUpdate(() => setLocalStorage());
</script>

<style>
  :global(body) {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
  }
</style>

<div class="App">
  <Navbar />
  {#if showForm}
    <ExpenseForm name={setName} cost={setCost} {isEditing} />
  {/if}
  <ExpenseList expenses={expensives} />
  <Total title="Total Expenses" {total} />
  <button on:click={() => state.clear()}>Clear List</button>
</div>
