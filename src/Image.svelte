<script>
  import { onMount, onDestroy } from 'svelte'
  import { fabric } from 'fabric'

  export let canvas, image, scale

  let fabricImage

  onMount(() => {
    const scaleX = canvas.width / image.width
    const scaleY = canvas.height / image.height
    scale = Math.min(scaleX, scaleY, 1)

    fabricImage = new fabric.Image(image, {
      selectable: false,
      scaleX: scale,
      scaleY: scale
    })
    canvas.add(fabricImage)
    fabricImage.sendToBack()
  })

  onDestroy(() => {
    if (fabricImage) {
      canvas.remove(fabricImage)
      fabricImage.dispose()
    }
  })
</script>
