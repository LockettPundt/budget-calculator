<script>
  import { identity } from 'svelte/internal';
  import Expense from './Expense.svelte';
  import Title from './Title.svelte';
  export let expenses = [];
</script>

<section>
  <Title title="Expense List" />
  {#each expenses as item, i (item.id)}
    <Expense index={i + 1} {...item} />
  {:else}
    <h2>currently no expenses.</h2>
  {/each}
</section>
