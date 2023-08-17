# pomodoro-inversion

Inverted pomodoro timer.
Rather than alerting me at the ends of fixed cycles, I just tell the timer when I'm working vs taking a break.
I work until a natural switching point.
And then I break until I feel refreshed.
The timer tells me how long I've taken in each cycle.

This way I'm proactively managing my focus, rather than reactively following pomodoro notifications.

I find regular pomodoro a bit too rigid.
When I'm first getting into the groove, shorter work cycles are nicer.
Once I'm in flow, longer work cycles are nicer.
If I have a lot of meetings, pomodoro work cycles don't necessarily tile well with meeting schedule.

## Design

If I'm managing my work/rest cycles, why do I even need a timer?
For statistics of course.

Pomodoro inversion is essentially a modified split stopwatch.
- Show The running length of the current cycle.
- have a button for starting next cycle.
- after n cycles, give a hint for longer rest.
- Show the lengths of previous cycles.
- indicate which cycles are work vs rest.

## Focus, Rest, React, vs Work, Rest

Normal pomodoro uses "work" and "rest" cycles.

I think of "work" as in-flow work, and rest as a kind of focused recovery.
But there's a third state where I'm doing chores or reacting to environment.

So I rename "Work" to "Focus", and I add an additional cycle type, "React".
"Focus", "Rest", "React".

Naming is a work in progress.
Rest is clear and well-named, but the two types of work are tricky.
Other things I've considered...
- Work, Chores
- Focused Work, Unfocused Work

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
pnpm run dev

# or start the server and open the app in a new browser tab
pnpm run dev -- --open
```

## Building

To create a production version of your app:

```bash
pnpm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.
