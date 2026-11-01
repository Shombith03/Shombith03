# Shombith Chakraborty

> *"Do not go gentle into that good night."* — Dylan Thomas

Game systems, the engines under them, and the pipelines that ship them.

I work on **[Cosmic Shore](https://github.com/froglet-studio/Cosmic-Shore)** at Froglet Games — a real-time 3D multiplayer game — from its interface to its build pipeline. I'm also writing an engine that runs it without Unity.

Everything below links to the commits and pull requests behind it. **Owned** means I built and own the system; **shared** means I worked on it alongside others.

---

### Amoebius — a .NET 10 engine that runs Cosmic Shore without Unity

`owned` · 15 projects

A scene graph with reflective lifecycle discovery, a deterministic game loop, an injection container and a SOAP layer, all replacing their Unity counterparts. The game's real `Assets/_Scripts` compile against it with [zero errors](https://github.com/froglet-studio/Cosmic-Shore/commit/6a4ace506ca9d93ae349289743521df55de21672). It carries Netcode's own model [between processes](https://github.com/froglet-studio/Cosmic-Shore/commit/aeba7a882eb423f03af98dc6271c00d5f914c83c) over its own TCP transport and RPC routing, plays [online through UGS Lobby and Relay](https://github.com/froglet-studio/Cosmic-Shore/commit/01f582228d37ae69b06ae85648bb15e082def605) like the Unity build, and [matches its rendering](https://github.com/froglet-studio/Cosmic-Shore/commit/fa16d6115ebfd06440e69d9bd815e6639934a84c) down to a reimplementation of URP 17.3's Gaussian bloom.

An MCP server lets an agent build the game, start it, screenshot it, click, steer and read live values. Because the loop is deterministic, the engine also works as a controlled capture environment for trailers — exact repeatable runs instead of hand-flown takes.

[Dev log: building our own engine, one script at a time](https://www.froglet.games/blog/amoebius-our-own-engine/)

### Cosmic Shore

`owned`

**The UI, rebuilt** — architecture and look. The ship HUD moved onto subscriptions; [`4500bd949`](https://github.com/froglet-studio/Cosmic-Shore/commit/4500bd94900401be9b8c7cce90eecdb8d4002c45) cut `ShipHUDController` by ~300 lines into `HudSubscriptionSO` and per-ability views, then [`662e300ed`](https://github.com/froglet-studio/Cosmic-Shore/commit/662e300ed46206479ece25160692e9ad305158d5) deleted 2,591 lines of superseded scripts across 80 files. A new visual language followed across menus, the hangar, the arcade flow and the event feed.

**PlayFab to UGS** — anonymous sign-in and profiles, one `UGSDataService` for cloud save and data, a live `PlayerDataService` across every menu, leaderboards, Cloud Code and IAP with web checkout. PlayFab then came out entirely: 452 files, ~87,800 lines, after proving 209 GUIDs had zero inbound references.

**Analytics and consent** — Firebase replaced with one facade behind a consent and age gate, fanning out to UGS and a PostHog sink batched through an on-disk queue.

### Shipping

`owned` · four platforms, automated and scheduled

iOS to TestFlight from GitHub Actions, signing a Windows-made Xcode export on a macOS runner. Android release bundles with a pre-upload Play check. WebGL published to Cloudflare R2 and [playable now](https://www.froglet.games/play), where rollback is one file. Steam through Steamworks.NET.

The Unity CI job had never actually run — the runner label was never set, so every green build had been Python checks only. [`14129ba73`](https://github.com/froglet-studio/Cosmic-Shore/commit/14129ba73) replaced it with a guard that validates, compiles, and opens an autofix PR.

### Tooling

`owned`

**Froglet Compute** — a compute server that takes job requests through git, runs them, and writes each job's best result and a heartbeat back to the repo.

**cs-asset** — edits Unity scenes and prefabs and writes them back byte for byte, with no Unity involved. Verified across 2,030 files.

**The agent pipeline** — the skills and hooks that make agent work viable on a 4,700-file Unity project, and the `/ship` protocol for closing a branch out honestly. I work heavily with Claude Code; a further 1,952 commits landed through my pull requests that way. Directing that well is its own skill.

### froglet.games

`owned`

The studio site. Jekyll on GitHub Pages, Cloudflare Pages previews on every branch, Consent Mode v2, forms through Apps Script, WebGL served from R2, and a browser Studio where the team edits their own profiles — GitHub sign-in, every save a commit through the API. **[froglet.games](https://www.froglet.games/)**

---

C# · .NET 10 · Unity 6.3 LTS · URP and shaders · Unity Gaming Services · Silk.NET · Python · GitHub Actions · Cloudflare · PostHog · Jekyll · MCP

**[Portfolio](https://shombith03.github.io/shombith-portfolio/)** · [LinkedIn](https://www.linkedin.com/in/shombith/) · shombithofficial@outlook.com

Kolkata. Open to contract work on Unity multiplayer, tooling and pipelines.
