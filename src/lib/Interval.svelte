<script lang="ts">
  import type { Mode } from "$lib/mode";
  import prettyMilliseconds from 'pretty-ms'

  export let mode:Mode
  export let interval:number
</script>

<div>
  <span>{prettyMilliseconds(interval, {colonNotation: true, keepDecimalsOnWholeSeconds: true, secondsDecimalDigits: 2})}</span>
  <span>{mode}</span>
</div>
