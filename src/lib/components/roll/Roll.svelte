<script lang="ts">
  import RollPopup from "./RollPopup.svelte";
  let names = "";
  let strings = [];
  let showModal = false;

  const toggleModal = () => {
    showModal = !showModal;
  };

  const random = (strNames: string) => {
    strings = strNames.trim().replace(/(\r\n)|\r|\n/g, "\n").split(/\n+/g).filter((e) => e.length);
    if(strings.length) toggleModal();
  };
</script>

<div>
  <h1>Roll</h1>
  <label for="names">
    Add list of names to randomize (separated by line breaks)
  </label>
  <br />
  <textarea id="names" name="names" bind:value={names} rows="10" cols="20" />
  <br />
  <br />
  <button on:click={() => random(names)}> Randomize </button>
  <span
    class="modal"
    style={`display: ${showModal ? "block" : "none"}`}
  >
    <RollPopup bind:names={strings} on:close={toggleModal} />
  </span>
</div>

<style>
  /* The Modal (background) */
  .modal {
    /* Hidden by default */
    position: fixed; /* Stay in place */
    z-index: 1; /* Sit on top */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgb(0, 0, 0); /* Fallback color */
    background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
  }
</style>
