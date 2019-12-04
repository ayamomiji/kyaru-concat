<script>
  import { fabric } from 'fabric'
  import ImageLoader from './ImageLoader.svelte'
  import Canvas from './Canvas.svelte'
  import Image from './Image.svelte'
  import Head from './Head.svelte'
  import Footer from './Footer.svelte'

  let canvas, image, scale, heads = []
  let result

  function handleKeydown (e) {
    if (e.which === 8 || e.which === 46) { // backspace or delete key
      deleteSelected()
    }
  }

  function deleteSelected () {
    const activeObjects = canvas.getActiveObjects()
    activeObjects.forEach(activeObject => {
      if (activeObject.head) {
        heads = heads.filter(head => head.id !== activeObject.head.id)
      }
    })
  }

  function replaceImage (e) {
    image = e.detail.image
    heads = []
  }

  function addHead () {
    heads = [...heads, { id: Date.now() }]
  }

  function output () {
    const width = image ? image.width : canvas.width
    const height = image ? image.height : canvas.height

    const outputCanvas = new fabric.Canvas(document.createElement('canvas'), {
      width, height
    })
    // add original image
    if (image) {
      outputCanvas.add(new fabric.Image(image))
    } else {
      scale = 1
    }
    // add heads
    canvas.getObjects().filter(object => object.head).forEach(image => {
      outputCanvas.add(new fabric.Image(image.head.image, {
        scaleX: image.scaleX / scale,
        scaleY: image.scaleY / scale,
        left: image.left / scale,
        top: image.top / scale
      }))
    })
    result = outputCanvas.toDataURL('png')
  }

  function clearResult () {
    result = null
  }
</script>

<svelte:head>
  <link rel='stylesheet' href='https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css'
      integrity='sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh'
      crossorigin='anonymous'>
</svelte:head>

<svelte:body on:keydown={handleKeydown} />

<style>
  .result {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background-color: white;
    overflow-y: auto;
  }
</style>

<div class='container'>
  <h1>接頭霸王 v0.1</h1>
  <div class='form-row'>
    <div class='col form-group'>
      <label>選一張圖:</label>
      <ImageLoader on:load={replaceImage} />
    </div>
    <div class='col form-group'>
      <label>加頭:</label>
      <button class='btn btn-outline-secondary' on:click={addHead}>
        加一顆頭
      </button>
    </div>
    <div class='col form-group'>
      <label>下載並分享:</label>
      <button class='btn btn-outline-secondary' on:click={output}>
        下載圖片
      </button>
    </div>
  </div>
  <Canvas bind:canvas />
  <Footer />

  {#if canvas}
    {#if image}
      {#each [image] as image (image.src)}
        <Image {canvas} {image} bind:scale />
      {/each}
    {/if}

    {#each heads as head (head.id)}
      <Head {canvas} {head} />
    {/each}
  {/if}
</div>

{#if result}
  <div class='result'>
    <div class='container'>
      <div class='d-flex'>
        <div class='flex-fill'>完成了! 請對圖片按右鍵另存:</div>
        <button class='btn btn-primary' on:click={clearResult}>繼續編輯</button>
      </div>
      <img src={result} style='max-width: 100%;' />
    </div>
  </div>
{/if}
