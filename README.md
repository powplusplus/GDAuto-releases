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
frame-perfect, and back up when stuck. Every finished route is replayed in the real game before it is offered. If the
copy plays a level differently from the game, the run stops and says where, instead of offering a route that fails.

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

## Error codes

A run that stops, or a save that fails, shows a code. The Geode log (Geode settings, open the logs folder) has the
details.

| Code | What happened | What to do |
|---|---|---|
| GDA-101 | The level didn't start within a minute. | Retry. Close other heavy programs. |
| GDA-102 | The mod couldn't make its hidden copy of the level. | Retry; restart the game if it keeps happening. |
| GDA-103 | Two-player or platformer level on a game build the mod can't read those from. | Use Geometry Dash 2.2081. |
| GDA-104 | The game stopped playing the level. | Turn off mods that pause or freeze levels, then retry. |
| GDA-105 | An error while the run was going, often out of memory. | Close other programs and retry. If it keeps happening, report it with the log. |
| GDA-201 | Windows wouldn't start the search threads. | Restart the game. |
| GDA-202 | The mod couldn't copy everything in this level. | Retry. If it keeps happening, report it with the level ID. |
| GDA-203 | The level has random enter effects, and another mod owns the random numbers they need. | Turn off mods that change randomness, then retry. |
| GDA-204 | Not enough free memory (RAM and page file) for the search. | Close other programs, or let Windows grow its page file. |
| GDA-205 | The search reached a game function it has no copy of. | Report it with the level ID. |
| GDA-206 | Another error inside the search. | Report it with the level ID and the log. |
| GDA-301 | The game dies at a point where the search survives. | Turn off physics mods (speedhack, TPS or FPS changers). Otherwise report it with the level ID and the step. |
| GDA-302 | Six found routes played differently in the game. | As GDA-301. |
| GDA-303 | Found routes don't replay the same from the level start. | As GDA-301. |
| GDA-401 | The Windows save dialog failed. | Retry. The route is also kept in the mod's `found` folder. |
| GDA-402 | The macro file couldn't be written. | Save to another folder. The route is also kept in the mod's `found` folder. |

## Requirements

- Windows (64-bit), Geometry Dash 2.2081, Geode.
- Any CPU that runs the game. The search uses all cores but one, and fewer when free memory is short: each search
  thread needs about 300 MB to 600 MB on detailed levels.
- Works with Mega Hack and other bots for playing the saved macro. Mods that change physics while the search runs
  (speedhack, TPS or FPS changers) make found routes fail in the game: turn them off first. Noclip and similar mods
  are fine: the search sees deaths before they hide them.

## Tips

- Turn off **Show Live View** for the fastest search.
- Mods that change physics (speedhacks, TPS changes) can make a route replay differently. Turn them off first.

## Install

Requires Windows, Geometry Dash 2.2081 and Geode 5.10.1 or newer for that version.

Download `aimas.gdauto-bruteforce.geode` from the [latest release](https://github.com/powplusplus/GDAuto-releases/releases/latest) and put it in the `geode/mods` folder of the game, or install it from the Geode index once it is listed.

## Issues

Report bugs in the [issue tracker](https://github.com/powplusplus/GDAuto-releases/issues) with the level ID, the error code if there is one, and your Geode log.

This repository holds releases only. The source is not public.
