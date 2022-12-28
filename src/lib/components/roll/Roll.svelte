<script lang="ts">
  import IntrigueString from "./../utils/IntrigueString.svelte";
  let names = "";
  let result = [];
  let index = 0;

  const printNext = () => {
    index++;
  };

  const printAll = () => {
    index = result.length;
  };

  const random = (strNames: string) => {
    const strings = strNames.replace(/(\r\n)|\r|\n/g, "\n").split(/\n+/g);
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

<h1>Roll</h1>
<label for="names">
  Add list of names to randomize (separated by line breaks)
</label>
<br />
<textarea id="names" name="names" bind:value={names} rows="10" cols="20" />
{#if result.length}
  <br />
  <button on:click={printNext}> Next name </button>
  <button on:click={printAll}> Show all </button>
  <p>Your result is</p>
{:else}
  <br />
  <br />
{/if}
{#each result as name, i (name)}
  {#if i < index}
    <p style="font-size: 1.5rem;">
      <strong>{i + 1}.</strong>
      <IntrigueString inString={name} />
    </p>
  {/if}
{/each}
<button on:click={() => random(names)}>
  Randomize{result.length ? " again" : ""}
</button>
