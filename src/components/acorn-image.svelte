<script>
  import Acorn from './assets/acorn.svelte'
</script>

<div class="acorn-image">
    <svelte:component this={Acorn} style="width: 100%;" />      
</div>

<style>
  .acorn-image {
    width: 32%;
    height: 90%;
    box-sizing: border-box;
    padding: 5% 1% 1% 1%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin-left: -0.2em;
    opacity: 0.7;
  }
</style>