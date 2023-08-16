<script lang="ts">
  import prettyMilliseconds from 'pretty-ms'
  import {onDestroy} from 'svelte'

  enum Mode {
    Work   = 'Work',
    Chores = 'Chores',
    Rest   = 'Rest'
  }

  let intervals:[Mode,number][] = []
  let lastSplit = Date.now()
  let now = Date.now()
  let mode = Mode.Rest

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
    intervals = [[mode, now - lastSplit], ...intervals]
    lastSplit = now

    mode = nextMode
  }
</script>

<h1>Pomodoro Inversion</h1>

<div>
  <span>{mode}</span>
  <span>{prettyMilliseconds(interval)}</span>
</div>

<button on:click={() => split(Mode.Work)}>Work</button>
<button on:click={() => split(Mode.Chores)}>Chores</button>
<button on:click={() => split(Mode.Rest)}>Rest</button>

<h2>cycle history</h2>
{ #each intervals as [mode, interval], i }
  <div>
    <span>{mode}</span>
    <span>{prettyMilliseconds(interval)}</span>
  </div>
{ /each }
