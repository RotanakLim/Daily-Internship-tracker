# Internship Tracker

A static page (`index.html`) that lists Summer 2027 internships. A Claude Code scheduled task runs every morning in Anthropic's cloud, follows the instructions in `TASK.md`, and pushes updated data to `main`.

- `data/postings.json` – postings found by the daily task (starts as `[]`)
- `data/runs.json` – one entry per daily run
- `data/sample-postings.json` – fake postings for testing; open the page with `?sample=1` to see them
- Save / Applied / Skip are stored in your browser (localStorage), so they're per device and the daily task never overwrites them.

## Setup

1. **Push this folder to a GitHub repo** (default branch `main`).
2. **Connect GitHub to Claude** so the scheduled task can clone and push: open [claude.ai/code](https://claude.ai/code) and connect GitHub / install the Claude GitHub App on this repo.
3. **Enable Pages from main:** Settings → Pages → Build and deployment → Source **Deploy from a branch**, Branch **main**, folder **/ (root)** → Save. The site appears at `https://<user>.github.io/<repo>/`.
4. **Let the task open posting pages:** the Default cloud environment only reaches allowlisted domains (GitHub, package registries). At [claude.ai/code/routines](https://claude.ai/code/routines) → the task → **Edit** → **Advanced settings → Cloud environment** → settings icon → **Network access: Full** → Save.
5. **The scheduled task** runs daily on your Claude subscription (Pro/Max). Manage it at [claude.ai/code/routines](https://claude.ai/code/routines). Its cron is UTC-only, so it fires at 14:50 and 15:50 UTC and the prompt skips whichever fire isn't 7:50 AM Pacific (or already ran today).

## Running it

- **Automatically:** every day at 7:50 AM Pacific, year-round.
- **Manually:** open the task at [claude.ai/code/routines](https://claude.ai/code/routines) → **Run now**, or run `/schedule run` in Claude Code.

Each run opens as a session on claude.ai where you can read the summary (new postings by track, plus closed ones).

## Preview locally

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000/ (real data) or http://localhost:8000/?sample=1 (sample data). Opening `index.html` as a file won't work because the page fetches the JSON files.
