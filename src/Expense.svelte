<script>
  export let name;
  export let cost;
  export let index;
</script>

<style>
  article {
    margin: 10px 0;
    background-color: cadetblue;
    padding: 10px;
  }
</style>

<article>
  <div>
    <h2>{index}. {name} <button> more </button></h2>
    <h4>amount: ${cost}</h4>
  </div>
  <div><button> edit </button></div>
</article>
