<script lang="ts">
  import * as tf from "@tensorflow/tfjs"
  import { onMount } from "svelte"

  let canvas: HTMLCanvasElement

  onMount(async () => {
    const grayAlpha = tf.fill<tf.Rank.R3>([200, 200, 4], 0.5)

    await tf.browser.toPixels(grayAlpha, canvas)
    console.log("tensor used", tf.memory().numTensors)
    grayAlpha.dispose()
    console.log("tensor cleaned", tf.memory().numTensors)
  })
</script>

<canvas width="200" height="200" bind:this={canvas} />
