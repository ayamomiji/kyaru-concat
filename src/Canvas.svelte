<script>
  import { onMount } from 'svelte'
  import { fabric } from 'fabric'

  export const width = Math.min(screen.width, 1140)
  export const height = width * 0.75
  export let canvas

  let canvasEl

  onMount(() => {
    canvas = new fabric.Canvas(canvasEl, {
      width, height,
      preserveObjectStacking: true
    })

    const bringToFront = event => {
      event.selected.forEach(selected => canvas.bringToFront(selected))
    }

    canvas.on('selection:created', bringToFront)
    canvas.on('selection:updated', bringToFront)
  })
</script>

<canvas bind:this={canvasEl} />
