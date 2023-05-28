<script lang="ts">
  import * as tf from "@tensorflow/tfjs"
  import { onMount } from "svelte"

  let canvas: HTMLCanvasElement

  onMount(async () => {
    const noise = tf.randomUniform<tf.Rank.R3>([200, 200, 1])

    await tf.browser.toPixels(noise, canvas)
    console.log("tensor used", tf.memory().numTensors)
    noise.dispose()
    console.log("tensor cleaned", tf.memory().numTensors)
  })
</script>

<canvas width="200" height="200" bind:this={canvas} />
