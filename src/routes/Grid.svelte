<script lang="ts">
  import { createEventDispatcher } from "svelte/types/runtime/internal/lifecycle";
  import Square from "./Square.svelte";

  export let grid: string[];
  export let found: string[];

  let a = -1;
  let b = -1;
  let reset_timeout: number;

  const dispatch = createEventDispatcher();
</script>

<div class="grid">
  {#each grid as emoji, i}
    <Square
      {emoji}
      on:click={() => {
        clearTimeout(reset_timeout);
        if (a === -1 && b === -1) {
          a = i;
        } else if (b === -1) {
          if (grid[a] === grid[b]) {
            dispatch("found");
            // correct
          } else {
            // incorrect
            reset_timeout = setTimeout(() => {
              a = b = -1;
            }, 1000);
          }
        } else {
          b = -1;
          a = 1;
        }
      }}
      selected={a === i || b === i} 
      />
  {/each}
</div>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);
    grid-gap: 0.5em;
    height: 100%;
  }
</style>
