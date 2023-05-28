<script lang="ts">
  import * as tf from "@tensorflow/tfjs"
  import { onMount } from "svelte"

  let canvas: HTMLCanvasElement

  onMount(async () => {
    // 2×2の格子模様
    const checky = tf.tensor3d([
      [[1], [0]],
      [[0], [1]]
    ])
    // 100×100のタイル状に敷き詰める（画像は200×200になる）
    const pattern = checky.tile<typeof checky>([100, 100, 1])

    await tf.browser.toPixels(pattern, canvas)
    console.log("tensor used", tf.memory().numTensors)
    tf.dispose([checky, pattern])
    console.log("tensor cleaned", tf.memory().numTensors)
  })
</script>

<canvas width="200" height="200" bind:this={canvas} />
