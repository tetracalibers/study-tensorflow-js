<script lang="ts">
  import * as tf from "@tensorflow/tfjs"
  import { onMount } from "svelte"

  let canvas: HTMLCanvasElement

  onMount(async () => {
    /** [height, width, color_dimension] */
    const black = tf.zeros<tf.Rank.R3>([100, 200, 3])

    await tf.browser.toPixels(black, canvas)
    console.log("tensor used", tf.memory().numTensors)
    black.dispose()
    console.log("tensor cleaned", tf.memory().numTensors)
  })
</script>

<canvas width="200" height="100" bind:this={canvas} />
