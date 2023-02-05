<script>
  import calculateWinner from "./lib/calculateWinner";
  import Square from "./lib/Square.svelte";
  let squares = new Array(9).fill(null);
  let xIsNext = true;
  let winner,
    status = "Next player: " + (xIsNext ? "X" : "O");
  let history = [];

  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) return;
    const newArr = [...squares];
    newArr[i] = xIsNext ? "X" : "O";
    squares = newArr;
    xIsNext = !xIsNext;
    history = [...history, newArr];
    winner = calculateWinner(squares);
    if (winner) {
      status = "Winner: " + winner;
    } else {
      status = "Next player: " + (xIsNext ? "X" : "O");
    }
  }
  function handleHistory(index) {
    squares = history[index];
  }
</script>

<main class="wrapper">
  <div class="container">
    {#each squares as item, i (i)}
      <Square value={item} handleClick={() => handleClick(i)} />
    {/each}
  </div>
  <div class="history">
    {#each history as h, i (i)}
      <button on:click={() => handleHistory(i)} class="step">go to step #{i + 1}</button>
    {/each}
  </div>
</main>

<p>{status}</p>

<style>
  .wrapper {
    display: flex;
  }
  .container {
    width: 310px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    margin-right: 50px;
  }
  .history{
    display: flex;
    flex-direction: column;
  }
  .step{
    margin-bottom: 10px;
  }
</style>
