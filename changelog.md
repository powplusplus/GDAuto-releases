# Changelog

## v1.0.1

- Levels with animated objects that fade out when they leave the screen (for example Dash) are searched on all CPU
  cores again.
- Every game function the search can reach is now ported.
- The floor and ceiling of ship, UFO, wave, swing and ball sections slide in exactly like in the game. The search used
  to keep them where they were when the run started, so routes through those sections could fail in the game.
- The slow one-thread search inside the game is gone. If the search can't play a level exactly like the game, the
  run stops and says why.
- Every stopped run and failed save shows an error code (GDA-101 to GDA-402), listed with what to do in the mod's
  description.
- Running out of memory during a run stops it with a message instead of closing the game.

## v1.0.0

First public release.

- Searches classic, two-player and platformer levels for a route, from a level's page or the page of one of your own
  levels.
- The search runs on all CPU cores but one, in the mod's own copy of the game's physics and triggers. A level it cannot
  play there is searched inside the game on one thread.
- Every found route is replayed in the game from a real restart before it is offered. Save it as .gdr2 or .mhr
  (platformer: .gdr2 only), or watch it.
- Live view: the level plays the furthest route found so far while the search runs.
- Input Timing FPS from 1 to 6000 for the search and the saved macro.
- Per-level CPS cap with spaced clicks, and per-level IL Mode (a 6000 FPS search for frame-perfect inputs), both in
  the level's options next to Low Detail Mode.
- Fewest Clicks removes clicks a found route does not need.
- Worker Load sets how much CPU the search uses while the live view is shown. Workers run below the game's priority.
- Macro Replay Compatibility (on by default) gives normal attempts the same object variance seed, enter effect
  randomness and custom hitbox offsets as the search, so saved macros replay the same. Turn it off to leave normal
  play untouched.
- A run does not change stats, attempts, jumps, quests, achievements or level completions.
