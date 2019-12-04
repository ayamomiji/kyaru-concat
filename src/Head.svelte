<script>
  import { onMount, onDestroy } from 'svelte'
  import { fabric } from 'fabric'
  import kyaru from './images/kyaru.png'

  export let canvas, head

  let fabricImage

  onMount(() => {
    const image = new Image()
    image.src = kyaru
    image.onload = function () {
      fabricImage = new fabric.Image(image, {
        rotatingPointOffset: 15,
        cornerStyle: 'circle'
      })
      fabricImage.setControlVisible('ml', false)
      fabricImage.setControlVisible('mt', false)
      fabricImage.setControlVisible('mr', false)
      fabricImage.setControlVisible('mb', false)
      canvas.add(fabricImage)
      canvas.centerObject(fabricImage)
      canvas.setActiveObject(fabricImage)
    }
  })

  onDestroy(() => {
    if (fabricImage) {
      canvas.remove(fabricImage)
      fabricImage.dispose()
    }
  })
</script>
