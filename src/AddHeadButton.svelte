<script>
  import { createEventDispatcher } from 'svelte'

  export let source

  const dispatch = createEventDispatcher()

  function addHead () {
    dispatch('add', { head: { id: Date.now(), source } })
  }
</script>

<style>
  .add-head-button {
    cursor: pointer;
    display: inline-block;
    flex-basis: 50px;
    opacity: 0.5;
    transition: opacity 0.3s ease;
  }

  .add-head-button:hover {
    opacity: 1;
  }

  img {
    width: 50px;
    height: 50px;
    object-fit: cover;
  }
</style>

<div class='add-head-button' on:click={addHead}>
  <img src={source} />
</div>
