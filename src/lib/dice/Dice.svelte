<script lang="ts">
    let num: number = 0;
    let max = 6;
    const random = () => {
      num = Math.floor(Math.random() * max) + 1;
    }
  </script>
  <!--  -->
  <h1>Dice</h1>
  <label for="maxNum">Max. number to randomize to</label><br>
  <input id="maxNum" name="maxNum" type="number" bind:value={max} />
  <p>Your random number is</p>
  <p style="font-size: 3rem;"><strong>{num}</strong></p>
  <button on:click={random}>
    Roll dice
  </button>
  