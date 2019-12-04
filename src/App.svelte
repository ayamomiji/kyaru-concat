<script>
	import { onMount } from 'svelte'
	import { fabric } from 'fabric'
	import ImageLoader from './ImageLoader.svelte'

	const width = 640, height = 480

	let canvasEl
	let canvas, image

	onMount(() => {
		canvas = new fabric.Canvas(canvasEl, { width, height })
	})

	function replaceImage (e) {
		if (image) {
			canvas.remove(image)
			image.dispose()
		}
		const scaleX = width / e.detail.image.width
		const scaleY = height / e.detail.image.height
		const scale = Math.min(scaleX, scaleY, 1)

		image = new fabric.Image(e.detail.image, {
			selectable: false,
			scaleX: scale,
			scaleY: scale
		})
		canvas.add(image)
	}
</script>

<svelte:head>
	<link rel='stylesheet' href='https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css'
			integrity='sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh'
			crossorigin='anonymous'>
</svelte:head>

<div class='container'>
	<ImageLoader on:load={replaceImage} />
	<canvas bind:this={canvasEl} />
</div>
