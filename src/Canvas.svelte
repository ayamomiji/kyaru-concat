<script>
  import { onMount } from 'svelte'
  import { fabric } from 'fabric'

  export const width = Math.min(screen.width, 1140)
  export const height = width * 0.75
  export let canvas

  let canvasEl

  onMount(() => {
    canvas = new fabric.Canvas(canvasEl, { width, height })
  })
</script>

<canvas bind:this={canvasEl} />
