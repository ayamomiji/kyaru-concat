<script>
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()

  let fileInput, urlInput

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

  function loadURL () {
    dispatchImage(urlInput.value)
    urlInput.value = null
  }

  function dispatchImage (src) {
    const image = new Image()
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

<div class='input-group'>
  <input type='text' class='form-control' placeholder='或者輸入圖片網址...'
      bind:this={urlInput} />
  <div class='input-group-append'>
    <button class='btn btn-outline-secondary' on:click={loadURL}>
      讀取網址
    </button>
  </div>
</div>
