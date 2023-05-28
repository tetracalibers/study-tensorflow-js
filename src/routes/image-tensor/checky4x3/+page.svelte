<script lang="ts">
  import * as tf from "@tensorflow/tfjs"
  import { onMount } from "svelte"

  let canvas: HTMLCanvasElement

  onMount(async () => {
    const checky4x3 = tf.tensor3d([
      [[1], [0], [1], [0]],
      [[0], [1], [0], [1]],
      [[1], [0], [1], [0]]
    ])

    await tf.browser.toPixels(checky4x3, canvas)
    console.log("tensor used", tf.memory().numTensors)
    checky4x3.dispose()
    console.log("tensor cleaned", tf.memory().numTensors)
  })
</script>

<canvas width="4" height="3" bind:this={canvas} />
