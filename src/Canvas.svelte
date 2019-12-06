<script>
  import { onMount } from 'svelte'
  import { fabric } from 'fabric'

  export const width = Math.min(window.width, 1140)
  export const height = width / 3
  export let canvas

  let canvasEl

  onMount(() => {
    canvas = new fabric.Canvas(canvasEl, { width, height })
  })
</script>

<canvas bind:this={canvasEl} />
