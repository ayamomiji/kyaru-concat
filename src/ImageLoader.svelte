<script>
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()

  let input

  function loadImage (e) {
    const reader = new FileReader()
    reader.onload = function (event) {
      const image = new Image()
      image.src = event.target.result
      image.onload = function () {
        dispatch('load', { image })
      }
    }
    reader.readAsDataURL(e.target.files[0])
    e.target.value = null
  }

  function triggerInput () {
    input.click()
  }
</script>

<input type='file' class='d-none' accept='image/*'
    on:change={loadImage}
    bind:this={input} />
<button class='btn btn-outline-secondary' on:click={triggerInput}>
  上傳圖片
</button>
