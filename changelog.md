# Changelog

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
