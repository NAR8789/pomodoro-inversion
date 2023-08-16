<script lang="ts">
  import type { Mode } from "$lib/mode";
  import prettyMilliseconds from 'pretty-ms'

  export let mode:Mode
  export let interval:number
</script>

<div>
  <span>{mode}</span>
  <span>{prettyMilliseconds(interval)}</span>
</div>
