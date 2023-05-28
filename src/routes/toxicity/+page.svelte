<script lang="ts">
  import * as toxicity from "@tensorflow-models/toxicity"
  import "@tensorflow/tfjs-backend-webgl"
  import { onMount } from "svelte"

  interface Prediction {
    label: string
    results: {
      probabilities: Float32Array
      match: boolean
    }[]
  }

  const threshold = 0.5

  let model: toxicity.ToxicityClassifier | null = null
  let sentence = ""
  let predictions: Prediction[] = []

  onMount(async () => {
    model = await toxicity.load(threshold, [])
  })

  const check = async () => {
    if (!model) return
    predictions = await model.classify(sentence)
    console.log(JSON.stringify(predictions, null, 2))
  }
</script>

<h1>Toxicity</h1>
<p>Enter a sentence to check if it's toxic.</p>
<input bind:value={sentence} />
<button on:click={check}>Check</button>

{#each predictions as prediction}
  <h2>{prediction.label}</h2>
  <ul>
    {#each prediction.results as result}
      <li>
        {result.match ? "✅" : "❌"}
        {result.probabilities[1].toFixed(2)}
      </li>
    {/each}
  </ul>
{/each}
