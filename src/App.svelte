<script>
    let keys = "12345";
    const interval = 1000;
    let listening = true;
    let buzzed = null;
    window.addEventListener("keydown", handleKeydown);
    function buzz(key) {
      if (listening && keys.includes(key)) {
            const pressedKey = key;
            const buttons = document.querySelectorAll("button");

            buttons.forEach((button) => {
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
    function handleKeydown(event) {
        buzz(event.key);
    }
</script>

<main>
    <h1>Buzzer</h1>
    <p>Enter the keys to be buzzed</p>
    <input type="text" name="keys" id="keys" bind:value={keys} />
    <div class="keys">
        {#each keys as key}
            <button buzzed={buzzed === key} on:click={() => buzz(key)}
                >{key}</button
            >
        {/each}
    </div>
</main>

<style>
    :global(:root) {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    }

    .keys {
    display: flex;
    flex-wrap: wrap; /* Enable flex wrap */
    gap: 10px; /* Use gap property for spacing between items */
}

button {
    flex: 0 0 calc(33.33% - 10px); /* Adjust the button width for three buttons per row */
    padding: 20px;
    border: 0;
    border-radius: 5px;
    width: 300px;
    height: 300px;
    font-size: 24px;
}

    button[buzzed="true"] {
        background-color: red;
    }

    input {
        margin-bottom: 10px;
    }

</style>
