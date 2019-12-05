<script>
  import { createEventDispatcher } from 'svelte'

  export let source

  const dispatch = createEventDispatcher()

  function addHead () {
    dispatch('add', { head: { id: Date.now(), source } })
  }
</script>

<button class='btn btn-outline-secondary' on:click={addHead}>
  <img src={source} width='50' />
</button>
