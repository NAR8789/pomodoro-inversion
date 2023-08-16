<script lang="ts">
  import {onDestroy} from 'svelte'

  let intervals:number[] = []
  let lastSplit = Date.now()
  let now = Date.now()

  $:interval = now - lastSplit
  $:working = intervals.length % 2 === 1

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

  function split() {
    now = Date.now()
    intervals = [now - lastSplit, ...intervals]
    lastSplit = now
  }
</script>

<h1>Pomodoro Inversion</h1>

<div>{interval}</div>

<button on:click={split}>{ working ? "rest" : "work" }</button>

<h2>cycle history</h2>
{ #each intervals as interval, i }
  <div>
    <span>{(intervals.length - i) % 2 === 0 ? "work" : "rest" }</span>
    <span>{interval}</span>
  </div>
{ /each }
