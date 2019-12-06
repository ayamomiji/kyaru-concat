<script>
  import { onMount, onDestroy } from 'svelte'
  import { fabric } from 'fabric'

  export let canvas, head, source

  let fabricImage

  onMount(() => {
    const image = new Image()
    image.src = head.source
    image.onload = function () {
      fabricImage = new fabric.Image(image, {
        head,
        rotatingPointOffset: 15,
        cornerStyle: 'circle',
        cornerColor: 'red',
        transparentCorners: false,
        borderColor: 'red'
      })
      fabricImage.setControlVisible('ml', false)
      fabricImage.setControlVisible('mt', false)
      fabricImage.setControlVisible('mr', false)
      fabricImage.setControlVisible('mb', false)
      canvas.add(fabricImage)
      canvas.centerObject(fabricImage)
      canvas.setActiveObject(fabricImage)

      head.image = image
    }
  })

  onDestroy(() => {
    if (fabricImage) {
      canvas.remove(fabricImage)
      fabricImage.dispose()
    }
  })
</script>
