# Stick Cricket

A single-file browser batting game. You bat from behind the stumps, chase a target, and every win unlocks a harder level. Pick your team and openers, play with just the four arrow keys, and your progress and scores are saved in the browser.

No install, no build step, no dependencies: it is one HTML file with inline CSS and JavaScript.

## Run it

1. Download `stick-cricket.html`.
2. Double-click it to open it in Chrome, Edge, Firefox or Safari on a laptop or desktop with a keyboard.

It works offline and from a `file://` path. It does not make any network requests.

## How to play

The bowler runs in on his own. A ring shows where the ball will meet your bat. It turns **green** when your timing is good. Press an arrow key as the ball reaches the ring.

| Key | Shot | Notes |
|-----|------|-------|
| ← | Leg side | Ground shot to the left. Can go for four. |
| → | Off side | Ground shot to the right. Can go for four. |
| ↑ | Lofted straight hit | Big reward (six) but risky: a mistimed loft is often caught. |
| ↓ | Block | Safe. Mostly dot balls and singles. |

Space or Enter starts the next ball early. Otherwise it starts by itself after a short pause.

What affects the result:

- **Timing.** The closer to the ring's centre, the better the shot. Too early can mean dot ball or bowled, too late means bowled, and not swinging at all means bowled.
- **Line.** The ball arrives on the leg side, straight, or the off side. Playing to the side it is heading for scores better than playing against it.
- **Fielding.** Higher levels have tighter fielders, which turn some boundaries into twos and some twos into singles.
- **Batter ratings.** Each player has a timing and a power rating. Timing widens or narrows your window. Power helps shots reach the boundary.

## Winning and levels

You win a level by reaching the target before you run out of balls or wickets. A win unlocks the next level. A loss lets you retry the same one. Any unlocked level can be replayed from the menu.

Difficulty rises each level: more runs needed per ball, a faster bowler, a narrower timing window, tighter fielders, and eventually fewer wickets.

| Level | Target | Balls | Wickets | Bowler speed | Timing window |
|-------|--------|-------|---------|--------------|---------------|
| 1 | 14 | 12 | 4 | 1.00× | widest |
| 2 | 17 | 12 | 4 | 1.12× | |
| 3 | 22 | 14 | 4 | 1.24× | |
| 5 | 32 | 16 | 3 | 1.48× | |
| 10 | 60 | 20 | 2 | 2.08× | narrow |

The required scoring rate is capped at 3.3 runs per ball, the bowler speed at 2.4×, and the timing window never shrinks below a small minimum. Wickets never drop below 2.

## Teams and players

Choose from India, Australia, England, South Africa, Pakistan and New Zealand. Each has an 11-player squad. You choose your two **opening batters**; the rest bat in squad order as wickets fall.

Player ratings (timing and power) are assigned by squad slot, not taken from real statistics, so they are a game mechanic rather than a reflection of any real player.

## Saved data

Everything is stored in the browser's `localStorage` under the key `stickcricket.v1`:

- last team and openers chosen
- highest unlocked level
- best score for each level
- the last 30 innings (level, team, result, score, date)

Notes:

- Data is saved per browser and per file location. Opening the game in a different browser, or from a different folder, starts fresh.
- Clearing the browser's site data erases it.
- The **Clear saved data** link on the menu resets everything.
- If the browser blocks storage, the game still plays but nothing is remembered.

## Customising

Everything lives in the `<script>` block of `stick-cricket.html`.

- **Teams and squads:** the `T` object near the top (team colour, then 11 comma-separated names).
- **Player ratings:** the `SK` (timing) and `PW` (power) arrays, indexed by squad slot.
- **Difficulty curve:** the `cfg(n)` function (balls, target, wickets, bowler speed, timing window, fielding).
- **Shot outcomes:** the `hit()` function.
- **Camera and stadium:** the constants at the top of the game section (`HZ`, `F`, `HC`) and the `buildBG()` function.

## Known limitations

- Keyboard only. There are no touch or mouse controls.
- Batting only: there is no bowling mode and no two-player mode.
- Fielders are scenery. They do not move or catch the ball. Outcomes are decided by the timing, line and shot rules above.
- The lettering painted on the pitch uses a system font, so its spacing may differ slightly between machines.

## Credits

Inspired by the browser game Stick Cricket. This is an independent re-creation with its own code and artwork.
