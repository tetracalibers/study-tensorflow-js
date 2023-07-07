<script lang="ts">
  import * as tf from "@tensorflow/tfjs"
  import { onMount } from "svelte"

  let img: HTMLImageElement
  let canvas: HTMLCanvasElement

  onMount(async () => {
    const original = tf.browser.fromPixels(img)
    const flipped = tf.reverse(original, 1)

    await tf.browser.toPixels(flipped, canvas)
    console.log("tensor used", tf.memory().numTensors)
    tf.dispose([original, flipped])
    console.log("tensor cleaned", tf.memory().numTensors)
  })
</script>

<img alt="" src="/autumn-leaves_00037.jpg" bind:this={img} />
<canvas bind:this={canvas} />
