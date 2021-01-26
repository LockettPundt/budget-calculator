<script>
  import { onMount } from 'svelte';
  let users = [];
  let loading = true;
  onMount(async () => {
    const response = await fetch('https://api.github.com/users');
    const data = await response.json();
    users = data;
    loading = false;
  });
</script>

{#if loading}
  <h2>Loading...</h2>
{:else}
  <section>
    {#each users as { login, html_url, avatar_url }, i (login)}
      <article>
        <img src={avatar_url} alt="github user avatar" />
        <p>{login}</p>
        <a href={html_url}>{login}</a>
      </article>
    {/each}
  </section>
{/if}

<style>
</style>
