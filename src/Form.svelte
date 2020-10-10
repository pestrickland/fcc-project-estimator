<script>
  export let id = 1
  export let name = "";
  export let price;

  $: mode = id ? "edit" : "add";
  $: canSubmit = price >= 0 && name !== "";

  function submit() {
    if (!canSubmit) {
      return;
    }

    price = "";
    name = "";
    id = undefined;
  }

  function cancel() {
    price = "";
    name = "";
    id = undefined;
}
</script>

<style>
  button {
    margin-left: 20px;
  }
  button:disabled {
    cursor: not-allowed;
  }
</style>

<form on:submit|preventDefault={submit}>
  <fieldset>
    <label for="nameField">Material</label>
    <input
      bind:value={name}
      type="text"
      id="nameField"
      placeholder="Wood, glue, etc." />
    <label for="priceField">Price</label>
    <input
      bind:value={price}
      min="0"
      step="any"
      type="number"
      id="priceField"
      placeholder="Price" />
  </fieldset>
  <button
    class="float-right"
    disabled={!canSubmit}
    type="submit">{mode}</button>
  {#if mode === 'edit'}
    <button on:click={cancel} class="float-right" type="button">Cancel</button>
  {/if}
</form>
