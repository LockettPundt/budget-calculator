<script>
  import Title from './Title.svelte';
  import { getContext, onDestroy, onMount, afterUpdate, beforeUpdate } from 'svelte';
  const { add, edit, hideForm } = getContext('state');
  export let name = '';
  export let cost = 0;
  export let isEditing = false;

  // onMount(() => console.log('form has mounted'));
  // onDestroy(() => console.log('form is destroyed'));
  // beforeUpdate(() => console.log('before update'));
  // afterUpdate(() => console.log('after update'));
  $: empty = !name || !cost;

  const onSubmit = () => {
    const options = {
      name,
      cost,
    };
    if (isEditing) {
      edit(options);
    } else {
      add(options);
    }
    name = '';
    cost = 0;
    isEditing = false;
  };
</script>

<section>
  <Title title="Add Expense" />
  <form on:submit|preventDefault={onSubmit}>
    <div class="toggle">
      <button type="button" on:click={hideForm}>Close</button>
    </div>
    <div>
      <label for="name">Name</label>
      <input type="text" id="name" bind:value={name} />
      <label for="cost">Cost</label>
      <input type="number" id="cost" bind:value={cost} />
    </div>
    {#if empty}
      <p>please fill out all fields</p>
    {/if}
    <button disabled={empty} type="submit">
      {#if isEditing}Edit Expense{:else}Add Expense{/if}
    </button>
  </form>
</section>

<style>
  .toggle {
    display: flex;
    flex-direction: column;
  }
  .toggle > button {
    align-self: flex-end;
  }
  div {
    display: grid;
    grid-template-columns: 1fr;
  }
  p {
    color: red;
  }
  form {
    display: grid;
    grid-template-columns: auto;
  }
  form > button {
    justify-self: end;
  }
</style>
