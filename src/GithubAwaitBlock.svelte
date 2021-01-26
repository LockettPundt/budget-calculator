<script>
  import App from './App.svelte';

  async function getUsers() {
    const response = await fetch('https://api.github.com/users');
    return await response.json();
  }
</script>

{#await getUsers()}
  <h3>Loading...</h3>
{:then users}
  <section>
    {#each users as { login, html_url, avatar_url }, i (login)}
      <article>
        <img src={avatar_url} alt="github user avatar" />
        <p>{login}</p>
        <a href={html_url} target="_blank">{login}</a>
      </article>
    {/each}
  </section>
{/await}
