<script>
  import ImageLoader from './ImageLoader.svelte'
  import Canvas from './Canvas.svelte'
  import Image from './Image.svelte'

  let canvas, image

  function replaceImage (e) {
    image = e.detail.image
  }
</script>

<svelte:head>
  <link rel='stylesheet' href='https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css'
      integrity='sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh'
      crossorigin='anonymous'>
</svelte:head>

<div class='container'>
  <ImageLoader on:load={replaceImage} />
  <Canvas bind:canvas />

  {#if canvas && image}
    {#each [image] as image (image.src)}
      <Image {canvas} {image} />
    {/each}
  {/if}
</div>
