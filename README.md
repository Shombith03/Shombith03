<!-- Drop a wide image here, exported from the portfolio hero (the black hole
     and spacetime grid), ~1280x320. That is where the theme comes from;
     markdown has no CSS. Then delete this comment.
     ![](banner.png) -->
<img width="5840" height="3285" alt="pexels-jplenio-3262249" src="https://github.com/user-attachments/assets/6a5b6fb3-824d-4911-89ab-275eacf23cd4" />
Shombith Chakraborty

> *"Do not go gentle into that good night."* — Dylan Thomas

Game systems, the engines under them, and the pipelines that ship them.

I work on **Cosmic Shore** at Froglet Games, from its interface to its build pipeline, and I'm writing the engine it runs on.

**Owned** means I built and own the system. **Shared** means I worked on it alongside others.

<br>

## Cosmic Shore

A real-time 3D multiplayer game. → [repo](https://github.com/froglet-studio/Cosmic-Shore) · [play it in your browser](https://www.froglet.games/play)

**The UI, rebuilt** `owned`

Architecture and look. The ship HUD moved onto subscriptions — `ShipHUDController` cut by ~300 lines into `HudSubscriptionSO` and per-ability views, then 2,591 lines of superseded scripts deleted across 80 files. A new visual language followed across menus, the hangar and the arcade flow.

**PlayFab to UGS** `owned`

Anonymous sign-in and profiles, one `UGSDataService` for cloud save and data, leaderboards, Cloud Code and IAP with web checkout. PlayFab then came out entirely — 452 files, ~87,800 lines, after proving 209 GUIDs had zero inbound references.

**Analytics and consent** `owned`

Firebase replaced with one facade behind a consent and age gate, fanning out to UGS and a PostHog sink batched through an on-disk queue.

**Shipping, four platforms** `owned`

Automated and scheduled. iOS to TestFlight from GitHub Actions. Android release bundles with a pre-upload Play check. WebGL on Cloudflare R2, where rollback is one file. Steam through Steamworks.NET.

The Unity CI job had never actually run — the runner label was never set, so every green build had been Python checks only. Replaced with a guard that validates, compiles, and opens an autofix PR.

<br>

## Amoebius

The engine I'm building for Cosmic Shore, so it runs without Unity. `owned` · .NET 10, 15 projects

A scene graph with reflective lifecycle discovery, a deterministic game loop, an injection container and a SOAP layer, each replacing its Unity counterpart. The game's real `Assets/_Scripts` compile against it with zero errors.

It carries Netcode's own model between processes over its own TCP transport, plays online through the same UGS Lobby and Relay as the Unity build, and matches that build's rendering down to a reimplementation of URP 17.3's Gaussian bloom.

An MCP server lets an agent build the game, start it, screenshot it, click, steer and read live values. And because the loop is deterministic, the engine doubles as a controlled capture environment for trailers — exact repeatable runs instead of hand-flown takes.

→ [Dev log: building our own engine, one script at a time](https://www.froglet.games/blog/amoebius-our-own-engine/)

<br>

## Tooling

**Froglet Compute** — a compute server that takes job requests through git, runs them, and writes each job's best result and a heartbeat back to the repo.

**cs-asset** — edits Unity scenes and prefabs and writes them back byte for byte, no Unity involved. Verified across 2,030 files.

**The agent pipeline** — the skills and hooks that make agent work viable on a 4,700-file Unity project, and the `/ship` protocol for closing a branch out honestly. I work heavily with Claude Code; a further 1,952 commits landed through my pull requests that way. Directing that well is its own skill.

<br>

## froglet.games

The studio site. Jekyll on GitHub Pages, Cloudflare previews on every branch, WebGL served from R2, and a browser Studio where the team edits their own profiles — GitHub sign-in, every save a commit through the API. → [froglet.games](https://www.froglet.games/)

<br>

---

C# · .NET 10 · Unity 6.3 LTS · URP and shaders · Unity Gaming Services · Silk.NET · Python · GitHub Actions · Cloudflare · PostHog · MCP

[Portfolio](https://shombith03.github.io/shombith-portfolio/) · [LinkedIn](https://www.linkedin.com/in/shombith/) · shombithofficial@outlook.com

Kolkata. Open to contract work on Unity multiplayer, tooling and pipelines.
