# xn-fantasy-lol

A Discord bot for League of Legends pro-play pick'em. Drop it in your server,
let people submit weekly predictions, and track everyone's accuracy over the split.

> Originally **LCSbert**, built for the 2021 LCS Spring Split. The cached match
> data in `assets/` is from that era — see [Status](#status) before expecting it
> to pull live games.

## Commands

All commands use the `$` prefix.

| Command | What it does |
| --- | --- |
| `$sched [week]` | Show the schedule for a week, labelled by day. |
| `$lcs <15 picks>` | Save your 15 predictions (team acronyms) for the current week. |
| `$check [week]` | Show the predictions you saved for a week. |
| `$record` | Show your prediction accuracy, week by week. |
| `$servers` | List the servers the bot is connected to. |

## Layout

- `main.py` — the Discord bot: command handlers and embeds (`discord.py` 2.x).
- `lolseries.py` — the data layer. `LoLSeries` holds league-agnostic logic;
  `LCS` adds NA-specific bits and the PandaScore download helper.
- `assets/*.json` — cached schedule, results, team, and prediction data.

## Setup

```bash
pip install -r requirements.txt
cp secrets.json.example secrets.json   # then fill in your tokens
python main.py
```

`secrets.json` holds your Discord bot token and a [PandaScore](https://pandascore.co/)
API token. It is gitignored — never commit it. User predictions are written to
`assets/predictions.json` (also gitignored).

The bot needs the **Message Content** privileged intent enabled in the Discord
developer portal so it can read `$`-prefixed commands.

## Status

This is a nostalgia/maintenance restore of a 2021 project. The code now imports
and runs cleanly on modern `discord.py`, but the bundled match data is frozen at
the 2021 Spring Split and the week logic is hardcoded to that split. To run it
against a current season you'd need to re-point the PandaScore download helpers
and refresh the `assets/` data.
