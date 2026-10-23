# 🎯 COD KD Tracker

Track your Call of Duty kill/death ratio across **Warzone** and **Multiplayer**, match by match.

A static web app: no backend, no account, no build step. Your matches are stored in your browser, and you can host it free on GitHub Pages.

## Features

- **Separate Warzone and Multiplayer KD**, side by side, plus a combined figure
- **Log matches** with playlist, map, kills, deaths, assists, placement (Warzone) or result (Multiplayer), date, and notes
- **Live KD preview** while you type a match in
- **KD over time chart** showing cumulative KD per mode, with a goal line
- **Last 10 KD** compared with your overall KD (green when you're improving)
- **Highlights**: best game, positive-KD streak, average kills, best map, and kills needed to reach your goal KD
- **Filters** by mode and time range (today, 7 days, 30 days, all time)
- **Edit and delete** any match
- **Import and export** as CSV or JSON for backups or moving between devices
- **Sample data** button to preview the dashboard before logging real games
- Light and dark mode (follows your system), works on phones

## How to put it online (GitHub Pages)

1. Create a new **public** repository on GitHub.
2. Click **uploading an existing file** and drag in `index.html`, `README.md` and `LICENSE`. Click **Commit changes**.
3. Go to **Settings → Pages**. Under **Source**, choose **Deploy from a branch**, pick **main** and **/ (root)**, then **Save**.
4. After a minute or two your tracker is live at `https://<your-username>.github.io/<repo-name>/`.

To use it offline, just double-click `index.html`.

## How KD is calculated

```
KD = kills ÷ deaths
```

If deaths is 0, KD equals kills (the same convention the game uses). Overall KD is **total kills ÷ total deaths**, not an average of per-match KDs, so a 30-kill game counts for more than a 2-kill game.

A Warzone match counts as a win when placement is 1. A Multiplayer match counts as a win when its result is "Win".

## CSV format

Export a CSV to see the format, or build one yourself with these columns (header row required, order doesn't matter):

| Column      | Required | Example                     |
|-------------|----------|-----------------------------|
| `date`      | no       | `2026-10-23T20:15:00Z`      |
| `mode`      | yes      | `warzone` or `multiplayer`  |
| `playlist`  | no       | `Resurgence`                |
| `map`       | no       | `Rebirth Island`            |
| `kills`     | yes      | `12`                        |
| `deaths`    | yes      | `4`                         |
| `assists`   | no       | `3`                         |
| `placement` | no       | `1` (Warzone only)          |
| `result`    | no       | `win`, `loss`, `draw` (Multiplayer only) |
| `notes`     | no       | `Tried the new SMG build`   |

Rows with problems are skipped and listed after import; the rest still come in.

## Why manual logging?

Activision doesn't offer an official public stats API. The unofficial endpoints that older trackers used need your account's login cookie, change without notice, and are often locked down, so a tracker built on them breaks regularly and puts your account credentials in a third-party app. Logging matches yourself takes a few seconds per game, works for every title and mode, and keeps your data fully in your hands.

If you want to experiment with automated import, the cleanest place to add it is a new function that produces match objects and passes them through `KDStats.validateMatch()` inside `index.html`, the same path the CSV importer uses.

## Ideas for contributions

- Session view (group matches played in one sitting)
- Per-weapon or per-loadout tracking via tags
- Damage, headshots, and score fields
- Squad/teammate tracking for Warzone
- PWA support for installing on a phone home screen

## Disclaimer

Fan-made project, not affiliated with or endorsed by Activision. Call of Duty and Warzone are trademarks of their respective owners.

## License

[MIT](LICENSE)
