<script>
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()

  let fileInput

  function loadImage (e) {
    const reader = new FileReader()
    reader.onload = function (event) {
      dispatchImage(event.target.result)
    }
    reader.readAsDataURL(e.target.files[0])
    e.target.value = null
  }

  function triggerInput () {
    fileInput.click()
  }

  function dispatchImage (src) {
    const image = new Image()
    image.setAttribute('crossOrigin', 'anonymous')
    image.src = src
    image.onload = function () {
      dispatch('load', { image })
    }
  }
</script>

<input type='file' class='d-none' accept='image/*'
    on:change={loadImage}
    bind:this={fileInput} />
<button class='btn btn-outline-secondary' on:click={triggerInput}>
  上傳圖片
</button>
