<script>
  import { onMount } from 'svelte'
  import { fabric } from 'fabric'

  export const width = 640, height = 480
  export let canvas

  let canvasEl

  onMount(() => {
    canvas = new fabric.Canvas(canvasEl, { width, height })
  })
</script>

<canvas bind:this={canvasEl} />
