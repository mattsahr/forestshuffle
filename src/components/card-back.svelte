<script>
  import Tree from './assets/tree-svg.svelte'
</script>

<div class="card-back">
  <div class="tree-border">
    <svelte:component this={Tree} style="width: 40%;" />      
  </div>
</div>

<style>
  .card-back {
    width: 90%;
    height: 90%;
    box-sizing: border-box;
    padding-bottom: 4%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    border: solid 1px #56ac70;
    border-radius: 0.4em;
    box-shadow: 2px 4px 8px rgba(0, 100, 40, 0.3);

    --s: 4px; /* control the size*/
    --c1: #a2d56f;
    --c2: #92c56f;
    
    --c:var(--c1) calc(100% - 2px),#0000;
    --r:calc(2.414*var(--s));
    --p:calc(1.414*var(--s));
    --g:radial-gradient(var(--s),var(--c));
    background:
      radial-gradient(var(--r) at 0    0   ,var(--c)),
      radial-gradient(var(--r) at 0    100%,var(--c)),
      radial-gradient(var(--r) at 100% 0   ,var(--c)),
      radial-gradient(var(--r) at 100% 100%,var(--c)),
      var(--g),var(--g),var(--g),var(--g) var(--c2);
    background-position: 
      var(--r) var(--r),0 var(--p),var(--p) 0,
      calc(-1*var(--s)) calc(-1*var(--s));
    background-size: calc(2*var(--r)) calc(2*var(--r));

  }

  .tree-border {
    border: solid 2px #6b8;
    border-radius: 1em;
    box-sizing: border-box;
    opacity: 0.8;
    width: 88%;
    aspect-ratio: 1.1;
    max-height: 80%;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    background: #92db56;
    background: radial-gradient(
      circle,
      rgba(146, 219, 86, 1) 2%, 
      rgba(42, 199, 102, 1) 100%
    );
    box-shadow: inset 0px 0px 18px rgba(0, 60, 20, 0.1);
  }

</style>