<script>
  import { createEventDispatcher } from 'svelte'

  export let source

  const dispatch = createEventDispatcher()

  function addHead () {
    dispatch('add', { head: { id: Date.now(), source } })
  }
</script>

<button class='btn btn-outline-secondary mr-1 mb-1' on:click={addHead}>
  <img src={source} height='50' />
</button>
