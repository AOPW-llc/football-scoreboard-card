# Football Scoreboard Card

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://github.com/hacs/integration)
[![Validate](https://github.com/AOPW-llc/football-scoreboard-card/actions/workflows/validate.yml/badge.svg)](https://github.com/AOPW-llc/football-scoreboard-card/actions/workflows/validate.yml)

A Home Assistant dashboard card for NFL scores. It shows a week at a time,
Sunday to Saturday, with one column per day. Each column has a dropdown of that
day's games and shows the selected game's score, team stats, leaders and
division standings. Tap a team logo for that team's season stats against the
league leaders and the full AFC / NFC standings.

No integration, sensor or API key is needed. The card reads ESPN's public
scoreboard, game summary, standings and team statistics feeds straight from the
browser.

## Features

- **A week per screen.** The arrows move a week back or forward with a sliding
  carousel. Within the week, swipe or scroll through the days, or tap a day
  button (S M T W T F S) to jump to it.
- **Fits the screen.** By default the card shows as many whole days as fit
  across it, so no column is cut off. On a phone that's one day at a time. Or
  choose how many days to show (1–7).
- **Game dropdown per day.**
  - Started or finished: `Dallas (38) - Philadelphia (21) Final` or
    `Dallas (14) - Philadelphia (10) 7:42/3rd`
  - Not started: `Carolina v. Green Bay, 8:15 PM`
- **Game view.**
  - Both teams as `(seed) City Name`, with logos, records and the score.
  - Team stats side by side once the game has started, with the better number
    highlighted.
  - Passing, rushing and receiving leaders.
  - Tap the **Team stats** or **Leaders** heading to hide that section in every
    day column, and tap it again to bring it back. The browser remembers your
    choice.
  - The top 3 teams in each team's division.
  - Before kickoff: venue, TV and (optionally) the betting line.
- **Team view.** Tap a team logo to see:
  - The team's season stats against the league leader in each, with its league
    rank.
  - AFC and NFC standings by division, with seeds and win-loss records. Tap any
    team to switch to it.
- **Live updates.** Refreshes every 30 seconds while a game is on (or about to
  start), and every 5 minutes otherwise.
- **Game counts.** Each day shows how many games are on it, in gray.
- **Favorite team.** Optionally picks your team's game automatically on the
  days they play.

## Installation

### HACS (recommended)

1. In HACS, open the menu (⋮) → **Custom repositories**.
2. Add `https://github.com/AOPW-llc/football-scoreboard-card` with category
   **Dashboard**.
3. Search for **Football Scoreboard Card**, download it, and reload your
   browser.

### Manual

1. Download `football-scoreboard-card.js` from the
   [latest release](https://github.com/AOPW-llc/football-scoreboard-card/releases/latest).
2. Copy it to `/config/www/football-scoreboard-card.js`.
3. Go to **Settings → Dashboards → ⋮ → Resources** and add
   `/local/football-scoreboard-card.js` as a **JavaScript module**.

## Configuration

Add the card from the dashboard card picker (search "Football"). Everything can
be set in the visual editor. The card works best full width, for example in a
**Panel** view.

```yaml
type: custom:football-scoreboard-card
team: DAL
days: auto
refresh_interval: 30
show_odds: true
```

| Option | Default | Description |
|---|---|---|
| `team` | none | Favorite team's abbreviation (e.g. `DAL`, `GB`, `KC`). Its game is selected automatically on the days it plays. |
| `days` | `auto` | How many days of the Sunday–Saturday week show at once (`auto` or `1`–`7`). The rest of the week is a swipe or scroll away, and the arrows always move a whole week. See below. |
| `refresh_interval` | `30` | Seconds between refreshes while a game is live (10–300). |
| `show_odds` | `true` | Show the betting line before kickoff. |

### Days on screen

The card always works in Sunday–Saturday weeks. `days` only sets how many of
that week's days are on screen together:

- **`auto`:** as many columns at least 300px wide as fit. One day below 600px
  wide (phones), and up to the whole week on a wide screen.
- **`1`–`7`:** that many days. `7` shows the whole week with nothing to swipe.
  If the card is too narrow for that many readable columns (about 220px each),
  it shows as many as fit and the rest scroll.

The card measures its own width, not the device's, so the result also depends
on the dashboard layout. A **Panel** view gives the card the full width.
Masonry columns are narrow and usually leave room for only one day.

## Stats shown

**Game stats:** total yards, passing, rushing, first downs, 3rd down, 4th down,
red zone, turnovers, sacked, penalties, possession.

**Season stats in the team view:** points per game, points allowed, total yards,
passing yards, rushing yards, yards allowed, 3rd down %, turnover differential,
takeaways, sacks.

## Notes

- Times are shown in your browser's time zone. A game belongs to the day it
  kicks off locally.
- Seeds are the conference playoff seeds from ESPN's standings. Seeds 1–7 make
  the playoffs.
- ESPN's feeds are public but undocumented, and can change without notice.

## Disclaimer

This is an unofficial, fan-made card. It is not affiliated with, endorsed by or
sponsored by the NFL, its teams or ESPN. Team names and logos are trademarks of
their respective owners. Logos are loaded from ESPN at runtime and are not
included in this repository.

## License

[MIT](LICENSE)
