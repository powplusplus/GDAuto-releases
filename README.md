# GDAuto Bruteforce

Finds a route through a level by brute force and saves it as a macro for a replay bot.

This is a bot, a cheat-class tool: it plays the level, not you. Its runs do not change your stats, attempts, jumps,
quests, achievements or level completions.

## How to use

1. Open a level's page (download it first if needed). Your own levels have the button too.
2. Press the green chip button and choose **Start**.
3. The level plays the furthest route found so far, slowing down where the search has not got further yet.
4. A route that reaches the end is replayed in the game from a real restart to check it. Then choose **Save**,
   **Watch** or **Delete**.

Press **Stop** or Escape to end a run.

## How it searches

Worker threads on all CPU cores but one (fewer when memory is short) play the level in the mod's own copy of the game's
physics and triggers. They retry from the deepest safe point, narrow to single-step timing where an input has to be
frame-perfect, and back up when stuck. A level the workers cannot play is searched inside the game instead, on one
thread, which is much slower. Either way, every finished route is replayed in the real game before it is offered.

## Macros

- **.gdr2** (GDReplayFormat 2): classic, two-player and platformer levels. Mega Hack v9 plays these.
- **.mhr** (Mega Hack v8): classic and two-player levels, not platformer. Mega Hack v9 cannot load it.

The save dialog opens in the game's `replays` folder when it exists. If a saved macro replays a frame early or late,
adjust **Frame Offset** in the mod's settings.

**Input Timing FPS** takes any whole number from 1 to 6000 (default 240). The search, the route check, Watch and the
saved macro all use that rate, and a replay bot needs physics and input timing at the same rate. Above 240 the physics
run in finer steps and use more CPU. The display does not need to reach that frame rate.

## Clicks and CPS cap

Clicks a found route does not need are removed before it is checked (a tap that changes nothing, or a release and press
that holding would replace). **Fewest Clicks** in the mod's settings turns this off.

To cap the clicks per second for a level, open the level's options (the gear on its page, next to **Low Detail Mode**)
and turn on **GDAuto CPS Cap**. It asks for the cap (default 9) and is saved for that level. The route then never has
more clicks than that in any one second (both players together; platformer walking does not count). Clicks are also
spaced: presses in a burst are never closer than half the cap's interval (83 ms at 6 CPS), and no tap or gap between
taps is shorter than 40 ms (less at high caps).

## IL Mode

For levels built around frame-perfect inputs, open the level's options and turn on **GDAuto IL Mode**. The level is
then searched at 6000 FPS whatever **Input Timing FPS** says, trying every single step before a death. It is much
slower, and replaying the macro needs 6000 FPS physics.

## What it changes in normal play

With **Macro Replay Compatibility** on (the default), three things in normal attempts match the search, so that saved
macros replay the same:

- objects with a custom hitbox offset get it from the object's own position, rotation and scale;
- the random variance of advanced follow and area triggers starts from the same seed on every attempt;
- random enter effect directions start from the same random state on every attempt.

Turn the setting off to leave normal play untouched by the mod. During a search these always apply.

## Tips

- Turn off **Show Live View** for the fastest search.
- Mods that change physics (speedhacks, TPS changes) can make a route replay differently. Turn them off first.

## Install

Requires Windows, Geometry Dash 2.2081 and Geode 5.10.1 or newer for that version.

Download `aimas.gdauto-bruteforce.geode` from the [latest release](https://github.com/powplusplus/GDAuto-releases/releases/latest) and put it in the `geode/mods` folder of the game, or install it from the Geode index once it is listed.

## Issues

Report bugs in the [issue tracker](https://github.com/powplusplus/GDAuto-releases/issues) with the level ID and your Geode log.

This repository holds releases only. The source is not public.
