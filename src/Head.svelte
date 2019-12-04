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
      fabricImage = new fabric.Image(image)
      canvas.add(fabricImage)
    }
  })

  onDestroy(() => {
    if (fabricImage) {
      canvas.remove(fabricImage)
      fabricImage.dispose()
    }
  })
</script>
