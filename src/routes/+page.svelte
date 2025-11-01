<script>
  import CardBack from '../components/card-back.svelte';
  import ForestGlade from '../components/forest-glade.svelte';
  import Acorn from '../components/acorn-image.svelte'

  // 6 rows, 5 numeric columns
  let grid = $state([
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0],
  ]);

  // derived column sums
  let sums = $derived(
    grid[0].map((_, col) =>
      grid.reduce((acc, row) => acc + row[col], 0)
    )
  );
  let playerNames = $state(['','','','',''])
  const labels = [
    // [{text: 'Forest Shuffle'}, {}],
    [{card: true}, {}],
    [{card: true}, { boxArrow: 'top'}],
    [{card: true}, { boxArrow: 'bottom'}],
    [{ boxArrow: 'left'}, {card: true}, { boxArrow: 'right'}],
    [{image: 'forest_glade_1.png'}, {}],
  ]
  // {#each items as item, i}

</script>



<div class="score-sheet-wrapper">
  <div class="row header-row">
      <div class="cell label-cell game-title-wrap">
        <h4 class="game-title">Forest Shuffle</h4>
      </div>
    {#each grid[0] as value, colIndex}
      <div class="cell">
        <input
          class="player-name"
          type="text"
          step="1"
          bind:value={playerNames[colIndex]}
        />
      </div>
    {/each}
  </div>

  <!-- Five input rows -->
  {#each grid as row, rowIndex}
    <div class="row">
      <div class="cell label-cell">

        {#each labels[rowIndex] as label, labelIndex}

          {#if label.card}
            <div class="card-wrapper">
              <CardBack />
            </div>
          {/if}

          {#if label.image}
            <ForestGlade />
          {/if}

          {#if label.boxArrow}
            <div class="box-frame {label.boxArrow}">

              {#if label.boxArrow === 'top' || label.boxArrow === 'right'}
                <div class="arrow {label.boxArrow}"></div>
              {/if}

              <div class="box"> </div>

              {#if label.boxArrow === 'bottom' || label.boxArrow === 'left'}
                <div class="arrow {label.boxArrow}"></div>
              {/if}
              
            </div>
          {/if}
        {/each}
      </div>

      {#each row as value, colIndex}
        <div class="cell">
          <input
            type="number"
            step="1"
            bind:value={grid[rowIndex][colIndex]}
          />
        </div>
      {/each}
    </div>
  {/each}

  <!-- Final sum row -->
  <div class="row">
    <div class="cell label-cell label-sum">
      <div class="sum-symbol">∑</div>
      <Acorn />
    </div>
    {#each sums as sum, sumIndex}
      <div class="cell sum-cell">{sum}</div>
    {/each}
  </div>
</div>

<style>

  :global(body) {
    background: #765;
    margin: 0px;
  }


  .score-sheet-wrapper {
    height: 98vh;
    width: calc(100vw - 2vw);
    display: flex;
    flex-direction: column;
    justify-content: stretch;
    align-items: stretch;
    font-size: 20px;
    font-family: sans-serif;
    margin: 1vh 1vw;
  }
  .row {
    display: flex;
    margin-bottom: 1px;
    box-sizing: border-box;
    height: 14%;
    align-items: stretch;
  }

  .cell.label-cell.game-title-wrap {
    background: #006644;
    border-radius: 0.2em;
  }

  h4.game-title {
    font-size: 3.3em;
    line-height: 0.3;
    letter-spacing: -0.15em;
    color: #00cc77;
    text-shadow: 1px 1px 2px rgba(255, 255, 255, 0.9), 
      -1px -1px 2px rgba(255, 255, 255, 0.9);
    text-align: center;
    margin: 0 0.1em;
    font-weight: bold;
    background: #064;
    border-radius: 1em;
    box-shadow: 1px 1px 12px rgba(0, 256, 40, 1);
  }

  .box-frame {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .box-frame.top, .box-frame.bottom {
    flex-direction: column;
  }

  .box-frame .box {
    border: solid #394 1px;
    background: white;
    width: 0.6em;
    height: 50px;
    border-radius: 0.2em;
  }

  .box-frame.left {
    margin-right: -0.6em;
  }

  .box-frame.right {
    margin-left: -0.6em;
  }

  .box-frame.top .box, .box-frame.bottom .box {
    height: 20px;
    width: 30px;

  }



  .box-frame.top .box { margin-top: 0.4em; }
  .box-frame.right .box { margin: 0em 0.6em 0em -0.8em; }
  .box-frame.left .box { margin: 0em -0.8em 0em 0.4em; }
  .box-frame.bottom .box { margin-bottom: 0.4em; }


  .box-frame .arrow {
    width: 0;
    height: 0;
    border-left: 1em solid transparent;
    border-right: 1em solid transparent;
    border-bottom: 1em solid #ed9613;
  }

  .box-frame .arrow.bottom { transform: rotate(180deg); }
  .box-frame .arrow.right { transform: rotate(90deg); }
  .box-frame .arrow.left { transform: rotate(270deg); }



  .cell {
    width: 14%;
    height: calc(100% - 2px);
    display: flex;
    align-items: center;
    justify-content: center;
    border: solid #ddd;
    border-width: 0px 1px 0px 0px;
  }

  .cell.label-cell {
    width: 28%;
    font-weight: bold;
    background: #e8f0e0;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    border-right: solid 1px #886;
  }

  .cell.label-cell.label-sum {
    font-size: 3em;
    text-shadow: 6px 6px 12px rgba(0, 0, 0, 0.3);
    color: #052;
  }

  .card-wrapper {
    box-sizing: border-box;
    height: 100%;
    width: 40%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  input {
    width: 100%;
    height: 100%;
    text-align: center;
    font-size: 2em;
    border: none;
    outline: none;
    color: #bbb;
    text-shadow: 2px 1px 4px rgba(0, 0, 0, 0.2);
  }
  input[type=number]:hover::-webkit-inner-spin-button,
  input[type=number]:focus::-webkit-inner-spin-button {  
      width: 20px;
      height: 40px;
  }

  input.player-name {
    font-size: 1em;
    text-shadow: none;
    color: #008866;
  }

  .sum-cell {
    background: #f3f3f3;
    font-size: 2.4em;
    font-family: sans-serif;
  }

  @media screen and (max-width: 700px) {
    input { font-size: 1.6em }
    .sum-cell { font-size: 1.8em }
    h4.game-title { font-size: 3em; }
  }

  @media screen and (max-width: 600px) {
    input { font-size: 1.5em }
    .sum-cell { font-size: 1.7em }
    h4.game-title { font-size: 2.6em; }
  }
  @media screen and (max-width: 500px) {
    input { font-size: 1.4em }
    .sum-cell { font-size: 1.6em }
    h4.game-title { font-size: 2.5em; }
  }

  @media screen and (max-width: 400px) {
    input { font-size: 1.2em }
    .sum-cell { font-size: 1.4em }
    h4.game-title { font-size: 2.4em; }
  }

</style>

