<script>
  let keys = "12345";
  const interval = 1000;
  let listening = true;
  let buzzed = null;
  window.addEventListener("keydown", handleKeydown);

  function handleKeydown(event) {
    if (listening && keys.includes(event.key)) {
      const pressedKey = event.key;
      const buttons = document.querySelectorAll("button");
      buttons.forEach(button => {
        if (button.textContent === pressedKey) {
          buzzed = pressedKey;
        }
      });
      listening = false;

      setTimeout(() => {
        buzzed = null;
        listening = true;
      }, interval);
    }
  }

</script>

<main>
  <h1>Buzzer</h1>
  <p>Enter the keys to be buzzed</p>
  <input type="text" name="keys" id="keys" bind:value={keys} />
  <div class="keys">
    {#each keys as key}
      <button disabled buzzed={buzzed === key}>{key}</button>
    {/each}
  </div>
</main>

<style>
  :global(:root) {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }

  .keys {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 10px;
  }

  button[buzzed="true"] {
    background-color: red;
  }

  input {
    margin-bottom: 10px;
  }
</style>
