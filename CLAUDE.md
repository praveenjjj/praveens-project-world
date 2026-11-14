# Praveen's Project World — Claude Code Rules

Permanent rules for this repo. Read this and `PLAN.md` at the start of every session.

## 1. Goal
A browser-based 3D multiplayer portfolio world (Unity 6, URP, WebGL). Visitors open a
public link, log in, pick an avatar, walk a small low-poly hilly area and enter buildings —
one building per project from my CV — to see descriptions, images, video and a rotating
3D model. Other visitors are visible, there is global voice chat and friendly paintball
shooting (no damage/death).

**Philosophy:** start simple, build one small task at a time, keep the architecture boring
and maintainable. Never work on more than one PLAN.md task at once.

## 2. Your role & workflow (every task)
Act as senior Unity 6 tech lead, multiplayer engineer and WebGL optimisation engineer.

1. Read `CLAUDE.md` and `PLAN.md`. Check `git status`.
2. Find the next unchecked, unblocked task in `PLAN.md`.
3. Inspect the relevant scenes, prefabs, scripts and packages (Unity MCP where available).
4. If an SDK/package is involved, verify the current docs and compatibility — never assume an API exists.
5. Present a short plan: files to create/modify, approach, acceptance test.
6. **Wait for my approval.** (I switch Plan Mode on myself with Shift+Tab.)
7. Implement only the approved task.
8. Test (see §12). Report changed files, results and anything not verified.
9. Commit with a descriptive message, then tick the box in `PLAN.md`.
10. If blocked: write the blocker under the task in `PLAN.md`, propose the smallest fix, stop.

Never mark a task done unless its "Done when" test actually passed.

## 3. Tech stack
| Area | Choice |
|---|---|
| Engine | Unity 6 (6000.3.x), URP |
| Platform | WebGL (desktop + mobile browsers) |
| Hosting | GitHub Pages (`gh-pages` branch). Phase 1–5: local build pushed manually. Phase 6: GitHub Actions + game-ci |
| Multiplayer | Photon Fusion 2, **Shared Mode** |
| Voice | Vivox (Unity Gaming Services), via Unity Authentication + Unity Cloud project link |
| Backend | Supabase (Auth, Postgres, RLS, REST) |
| Content loading | Addressables, one group per building |
| Animation / art | Mixamo humanoid animations, Blender-optimised low-poly models |
| Video | MP4 files served from GitHub Pages `/videos`, Unity VideoPlayer in URL mode |
| Runtime model loading (if ever needed) | glTF via glTFast |

Rules:
- Do **not** use Mirror. Do not silently swap any technology.
- Unity Netcode for GameObjects 2.x + Distributed Authority is the only allowed fallback for
  Fusion. Before recommending it, report WebGL support, pricing, transport and limitations.
- No new third-party or paid packages without my approval.

## 4. Folder structure
Inspect before creating. Never delete or reorganise existing files without approval.

```
PraveensProjectWorld/            (repo root = Unity project root)
├── Assets/_Project/
│   ├── Art/{Environment,Characters,Materials,VFX}/   ← optimised, in-game assets only
│   ├── Audio/  Animations/  Settings/  UI/
│   ├── Prefabs/{Player,Buildings,UI}/
│   ├── Scenes/
│   ├── Scripts/{Core,Player,World,Projects,Networking,Voice,Backend,UI,Editor}/
│   └── ScriptableObjects/{Projects,Characters,Config}/
├── SourceAssets/                ← ORIGINAL raw files, OUTSIDE Assets/, gitignored
│   ├── Lobby_AboutMe/  BR1/  AR_Pump/  E_Kanban/  VR_Autism/
│   └── VR_Elearning/  PointCloud/  AR_Phonics/  AWG_OSHA/
├── Config/
│   ├── ProjectSecrets.example.json   ← placeholders, tracked
│   └── Local/ProjectSecrets.json      ← real values, gitignored
├── Documentation/  (SETUP_MAC.md, PROMPTS.md, decisions, limitations)
├── CLAUDE.md  PLAN.md  README.md  .gitignore
```
- `SourceAssets/` is never imported by Unity. Make optimised copies into `Assets/_Project/Art/`.
- Never commit files > 50 MB. Videos are published to the `gh-pages` branch under `/videos`, not imported into Unity.
- Namespace: `PraveensProjectWorld.<Area>` (e.g. `PraveensProjectWorld.Networking`).

## 5. C# conventions
- PascalCase: classes, methods, public properties, constants. camelCase: private fields.
  `[SerializeField] private` instead of public fields. Interfaces start with `I`.
- ScriptableObjects end in `Data` or `Config` (`ProjectData`, `ClientConfig`).
- Small focused MonoBehaviours, composition over inheritance, minimal singletons.
- Keep UI, gameplay, networking, voice and backend in separate scripts/asmdefs.
- Cache components, avoid per-frame allocations and needless `Update()` polling, pool frequent effects.
- No magic numbers — expose as serialized config. Handle missing refs and network errors gracefully.
- Don't suppress warnings you don't understand. Avoid over-engineering.

## 6. WebGL constraints (primary target, not an afterthought)
- Initial download target **< 50 MB**; building content via Addressables on demand.
- Enable **Decompression Fallback** (GitHub Pages can't set compression headers).
- No native plugins, no threads, no `System.Net.Http.HttpClient`, no raw sockets — use `UnityWebRequest`.
- Browser rules: mic only after a user click; video/audio autoplay only after a user click (or muted).
- Low-poly assets, compressed textures/audio, limited realtime lights and shadows, LODs where useful.
- Test in Chrome and Safari; mobile browsers in Phase 6.

## 7. World, player, buildings
- Small hilly terrain, gentle slopes, paths, minimal modern buildings, clean low-poly look.
- Third-person controller: walk, run, jump, follow camera, keyboard/mouse; touch controls (Phase 6).
- **One** reusable `ProjectBuilding` prefab driven by a `ProjectData` ScriptableObject:
  id, title, short + long description, image gallery, video URL, model reference/path,
  optional animation, metadata (company, year, award). No per-project building code.
- Inside: images on walls, video screen, model rotating on a central pedestal, optional animation.
- AR/VR projects are shown as video + 3D model (no real AR/VR in the browser).
- Building content is local (Addressables) and independent of multiplayer.

## 8. Multiplayer (Photon Fusion 2 Shared Mode)
- Spawn one networked player per visitor, sync movement/animation, name tags, online count.
- Paintball: local raycast + RPC so others see the splat. No health, damage or death.
- Only sync what must be shared; keep cosmetic effects local where possible.
- Photon App ID lives in Fusion's `PhotonAppSettings` asset (it's a public identifier, not a secret).

## 9. Voice (Vivox)
- One global 2D channel, explicit **Join Voice** button, mute/unmute, speaking indicator if supported.
- Known WebGL limits: one channel per instance, 2D only (no positional), no display names.
- Sign in via Unity Authentication (anonymous is fine). Keep voice independent of networking.

## 10. Backend (Supabase)
- Call Supabase **Auth and REST endpoints directly with `UnityWebRequest`** (no HttpClient-based SDK).
- Login = **email + 6-digit OTP code** (no magic-link redirects — they reload the WebGL page).
- Tables: `profiles` (id = auth user id, display_name, avatar_skin, company, role, email,
  created_at, updated_at), `access_control` (email, is_allowed, created_at),
  `world_settings` (id, is_open, updated_at).
- **Row Level Security ON** for every table. Users read/write only their own profile;
  `access_control` and `world_settings` are read-only to clients.
- Access gate: on login the client checks `world_settings.is_open` and the user's allowlist
  entry before connecting to Photon. Optional hardening (task 5.9b): Photon Custom
  Authentication backed by a Supabase Edge Function.

## 11. Secrets & config
- Real values: `Config/Local/ProjectSecrets.json` (gitignored). Placeholders: `Config/ProjectSecrets.example.json`.
- An editor script generates `Assets/_Project/ScriptableObjects/Config/ClientConfig.asset`
  from that JSON before builds (in CI: from GitHub Secrets). The generated asset is gitignored.
- Only public client values may ship in the build: Supabase URL + anon/publishable key, Photon App ID.
- **Never** put the Supabase service-role key, GitHub tokens or Unity license data in Unity or the repo.
- Never print secrets in logs, reports or commit messages.

## 12. Testing
- Every task has a "Done when" test in `PLAN.md`; run it before committing.
- WebGL features: build succeeds, runs in browser, console has no errors, performance OK.
- Multiplayer/voice: two browser tabs (or two browsers) — both spawn, see each other, hear each other.
- Supabase: valid login, invalid login, profile persists, blocked user, world closed/open.
- If you can't test something (no browser tool, needs my mic), say exactly what wasn't verified.

## 13. Git & deploy
- Check `git status` first; never overwrite my unrelated changes; never force-push.
- One task = one commit with a clear message. Never commit `Library/`, `Temp/`, `Logs/`,
  `UserSettings/`, `Builds/`, secrets or `SourceAssets/`.
- Deploy: WebGL build → `gh-pages` branch → test the **live URL**, not just the Editor.
- Don't change GitHub repo settings without approval.

## 14. Future — OpenUSD (OUT OF SCOPE NOW)
Do not install USD packages or build USD/Omniverse features yet. Keep compatible:
1 unit = 1 m, Y-up, originals kept in `SourceAssets/`, data-driven model references,
glTF for any runtime loading. Later: editor-only `com.unity.importer.usd` /
`com.unity.exporter.usd` pipeline, Omniverse export, an OpenUSD building.

## 15. Scope protection
No unrequested features: no inventory, economy, combat, analytics, extra backends or paid
packages. If something is unclear, ask before making architectural decisions.
