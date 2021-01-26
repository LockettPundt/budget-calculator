<script>
  import Expense from './Expense.svelte';
  import { quadInOut } from 'svelte/easing';
  import { fly } from 'svelte/transition';
  import Title from './Title.svelte';
  import { flip } from 'svelte/animate';
  export let expenses = [];
</script>

<section>
  <Title title="Expense List" />
  {#each expenses as item, i (item.id)}
    <div
      in:fly={{
        x: 100,
        y: 0,
        duration: 300,
        delay: i * 100,
        easing: quadInOut,
      }}
      out:fly={{
        x: -100,
        y: 0,
        duration: 300,
        delay: 100,
        easing: quadInOut,
      }}
      animate:flip={{
        delay: 50,
        duration: 500,
      }}
    >
      <Expense index={i + 1} {...item} />
    </div>
  {:else}
    <h2>currently no expenses.</h2>
  {/each}
</section>
