<script lang="ts">
  import Interval from '$lib/Interval.svelte';
  import Mode from '$lib/mode';
  import {onDestroy} from 'svelte'

  let intervals:[Mode,number][] = []
  let lastSplit = Date.now()
  let now = Date.now()
  let nowMode = Mode.Rest

  $:interval = now - lastSplit

  if (typeof requestAnimationFrame !== 'undefined') {
    let frame:number;
    (function tick() {
      now = Date.now()
      frame = requestAnimationFrame(tick)
    }())

    onDestroy(() => {
      cancelAnimationFrame(frame)
    })
  }

  function split(nextMode:Mode) {
    now = Date.now()
    intervals = [[nowMode, now - lastSplit], ...intervals]
    lastSplit = now

    nowMode = nextMode
  }
</script>

<h1>Pomodoro Inversion</h1>

<div>
  { #each Object.values(Mode) as mode }
    <button on:click={() => split(mode)} disabled={mode === nowMode}>{mode}</button>
  { /each }
</div>

<Interval mode={nowMode} interval={interval}/>
{ #each intervals as [mode, interval], i }
  <div>
    <Interval mode={mode} interval={interval}/>
  </div>
{ /each }
