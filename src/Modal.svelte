<script>
  export let showForm;
</script>

{#if showForm}
  <div class="overlay">
    <div class="modal">
      <div class="content">
        <slot />
      </div>
    </div>
  </div>
{/if}

<style>
  .overlay {
    position: absolute;
    display: grid;
    grid-template-columns: 1fr;
    align-content: center;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    z-index: 10;
    background-color: rgba(20, 20, 20, 0.5);
  }

  .modal {
    justify-self: center;
    border-radius: 3px;
    background-color: white;
    width: 400px;
    min-height: 200px;
    overflow: hidden;
  }

  .content {
    padding: 15px;
    margin: 30px 0;
  }
</style>
