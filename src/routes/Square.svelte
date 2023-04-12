<script lang="ts">
  export let emoji: string;
  export let selected: boolean;
 
</script>

<div class="square" class:flipped={selected}>
  <button on:click />

 
  <span>{emoji}</span>
</div>

<style>
  .square {
    background: yellow;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .flipped button {
    background: yellowgreen;
  }

  span {
    font-size: 5em;
    pointer-events: none;
  }
  button {
    position: absolute;
    height: 100%;
    width: 100%;
  }
</style>
