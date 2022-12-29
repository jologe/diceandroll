<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import IntrigueString from "../utils/IntrigueString.svelte";
  export let names = [];
  let result = [];
  let index = 0;
  const dispatch = createEventDispatcher();

  $: {
    random(names);
  }

  const close = () => {
    dispatch("close");
  };

  const printNext = () => {
    index++;
  };

  const printAll = () => {
    index = result.length;
  };

  const random = (strings: string[]) => {
    for (let i = 0; i < strings.length * 10; i++) {
      const num1 = Math.floor(Math.random() * strings.length);
      const num2 = Math.floor(Math.random() * strings.length);
      const temp = strings[num1];
      strings[num1] = strings[num2];
      strings[num2] = temp;
    }
    result = strings[0] ? strings : [];
    index = 0;
    printNext();
  };
</script>

<div class="modal-content">
  <span class="close" on:click={close}>&times;</span>
  <h1>Roll results</h1>
  <br />
  <div>
    <button on:click={printNext}> Next name </button>
    <button on:click={printAll}> Show all </button>
  </div>
  <p>Your result is</p>
  {#each result as name, i (name)}
    {#if i < index}
      <p style="font-size: 1.5rem;">
        <strong style="font-size: 1.2rem;">{i + 1}.</strong>
        <IntrigueString inString={name} />
      </p>
    {/if}
  {/each}
  <button on:click={() => random(names)}> Randomize again </button>
</div>

<style>
  /* Modal Content/Box */
  .modal-content {
    background-color: #fefefe;
    margin: 15% auto; /* 15% from the top and centered */
    padding: 20px;
    border: 1px solid #888;
    width: 80%; /* Could be more or less, depending on screen size */
  }

  /* The Close Button */
  .close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
  }

  .close:hover,
  .close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
  }
</style>
