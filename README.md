# TradingView MCP — Setup Package

This is the automated version of the setup from your PDF, split into three files
so the framework (script + config template) is ready now, and your personal
trading details stay separate and private until you fill them in.

## Files

| File | Purpose |
|---|---|
| `setup_tradingview_mcp.sh` | Runs steps 1–4 automatically: clone/update the MCP server, register it in `.mcp.json`, drop in the rules template, launch TradingView with the debug port. |
| `merge_mcp_config.js` | Helper used by the script — safely merges the `tradingview` entry into your existing `.mcp.json` without touching other MCP servers you've already set up. |
| `rules.template.json` | Your trading framework, with `<<PLACEHOLDER>>` fields for the personal details only you should fill in (account size, risk %, watchlist, preferences). |

## How to run it

1. Download all three files into one folder on your **local machine** (the one with TradingView Desktop and Claude Code installed — not this chat).
2. Open a terminal in that folder.
3. Run:
   ```bash
   chmod +x setup_tradingview_mcp.sh
   ./setup_tradingview_mcp.sh
   ```
   (On Windows, run it inside WSL or Git Bash — steps 1–3 need `git`/`node`/`npm`. Step 4, launching TradingView, you'll do separately in PowerShell as the script will tell you.)
4. The script creates `~/tradingview-mcp/rules.json` from the template. Open that file and replace every `<<...>>` placeholder with your real numbers — account size, max risk per trade, your actual watchlist, session preferences, anything you don't want to type out loud in a chat.
5. Open Claude Code in that folder and run `tv_health_check` to confirm the connection is live.

## Why it's split this way

- The script and template are the reusable "framework" — same for anyone.
- `rules.json` (generated locally, never uploaded anywhere) is where your personal trading details live. Nothing in this package transmits that file anywhere — it only sits on your disk and gets read by Claude Code locally when you ask it to scan charts.

## Before you rely on it

- The MCP server itself (`tradesdontlie/tradingview-mcp` on GitHub) is a third-party open-source project — worth skimming the source/issues once before connecting it to anything tied to real trades.
- The `--remote-debugging-port=9222` flag exposes whatever's on screen in TradingView to anything that connects to that port. It's local-only by default, but don't expose that port externally (e.g. via port forwarding) without understanding the implications.
- Treat the bias/risk rules in the template as a starting framework, not financial advice — they're the same example logic from the PDF and only as good as the numbers you put in.
