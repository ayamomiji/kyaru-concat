<script>
  import { onMount, onDestroy } from 'svelte'
  import { fabric } from 'fabric'

  export let canvas, head, flip, source

  let fabricImage

  onMount(() => {
    const image = new Image()
    image.src = head.source
    image.onload = function () {
      const scale = (canvas.width / 4) / image.width
      fabricImage = new fabric.Image(image, {
        head,
        rotatingPointOffset: 15,
        cornerStyle: 'circle',
        cornerColor: 'red',
        transparentCorners: false,
        borderColor: 'red',
        scaleX: scale,
        scaleY: scale,
        flipX: flip
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
