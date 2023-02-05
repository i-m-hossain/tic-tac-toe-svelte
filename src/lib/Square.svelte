<script>
  export let value, handleClick;
</script>

<button class="square" on:click={handleClick}>
  {value? value : ""}
</button>

<style>
  .square {
    border: 1px solid;
    padding: 20px;
    width: 100px;
    height: 100px;
    margin: 5px;
  }
</style>
