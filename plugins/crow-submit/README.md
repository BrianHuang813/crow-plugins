# crow-submit

A Claude Code plugin that submits your project to the [Crow Digital Darwinism grid](https://crow-eight.vercel.app) directly from your terminal — no browser required.

## What It Does

1. **Authenticates** via GitHub Device Flow (one-time setup; token cached at `~/.crow/token` for 30 days)
2. **Detects** your project name, description, URL, and tech stack from `package.json`, `pyproject.toml`, `Cargo.toml`, or `README.md`
3. **Lets you edit** any field before submitting
4. **Invites you to share a public GitHub repo** (opt-in) so others can collaborate and help your project survive — your git remote is never shared automatically, so private repos stay private
5. **Submits** to the grid and shows you the live link

## Install

In Claude Code:

```
/plugin marketplace add BrianHuang813/crow-plugins
/plugin install crow-submit@crow
```

## Usage

In any project directory, run:

```
/crow-submit:submit
```

Or just describe what you want — the skill auto-invokes on prompts like "submit my project to crow".

## First Run

On first use, you'll see:

```
  ╔══════════════════════════════════════════╗
  ║  GitHub Authorization Required           ║
  ╠══════════════════════════════════════════╣
  ║  1. Open:  https://github.com/login/device
  ║  2. Enter: ABCD-1234
  ╚══════════════════════════════════════════╝

  Waiting for authorization.......
  ✓ Logged in as @yourhandle
```

Your token is saved and reused for 30 days.

## Configuration

| Variable | Default | Purpose |
|---|---|---|
| `CROW_API_URL` | `https://api-production-1f00d.up.railway.app` | Override the backend API (e.g. local dev) |
| `CROW_WEB_URL` | `https://crow-eight.vercel.app` | Override the web app (used for the project link shown after submit) |

```bash
# Point at a local backend
CROW_API_URL=http://localhost:8000 claude
```

## Troubleshooting

**"Token expired — re-authenticating..."**
Your 30-day token expired. The skill handles this automatically and re-runs Device Flow.

**"Grid is currently full"**
All 3600 cells are occupied. Check back in a few hours — projects die from inactivity.

**"You already have an active project"**
Each user can have one project at a time. The skill offers to abandon your current one before submitting a new one.
