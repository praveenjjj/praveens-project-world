# Praveen's Project World — Development Plan

Unity 6 (6000.3.x) · URP · WebGL · part-time 2–3 h/day · prototype target 3–4 weeks
Work top to bottom. Tick a box only when its **Done when** test passes. Write blockers under the task.

## Phase 0 — Setup & verification (read-only, no gameplay code)
- [ ] 0.1 Confirm Unity version + URP template. **Done when:** ProjectVersion.txt shows 6000.3.x and URP asset is active.
- [ ] 0.2 Confirm WebGL Build Support installed. **Done when:** WebGL can be selected as build target.
- [ ] 0.3 Confirm git repo + remote. **Done when:** `git status` clean, `origin` points to GitHub repo.
- [ ] 0.4 Confirm `gh auth status`. **Done when:** authenticated to my GitHub account.
- [ ] 0.5 Confirm Unity MCP connection. **Done when:** a read-only Unity MCP tool (e.g. list scenes/console) returns data.
- [ ] 0.6 Confirm Supabase MCP connection. **Done when:** project is visible without printing keys.
- [ ] 0.7 Compare folders with CLAUDE.md §4. **Done when:** missing folders listed (create only after approval).
- [ ] 0.8 Confirm `.gitignore` covers Library/Temp/secrets/SourceAssets. **Done when:** `git check-ignore` passes for each.
- [ ] 0.9 Confirm `Config/Local/ProjectSecrets.json` exists with real values (don't print them). **Done when:** keys present, non-placeholder.
- [ ] 0.10 Compatibility audit: Fusion 2 Shared + WebGL, Vivox + WebGL, Supabase via UnityWebRequest, Addressables on GitHub Pages. **Done when:** short report with risks in `Documentation/COMPATIBILITY.md`.

## Phase 1 — Vertical slice (live link)
- [ ] 1.1 Create `Main` scene. **Done when:** loads with no console errors.
- [ ] 1.2 Terrain with gentle hills. **Done when:** player can walk everywhere without getting stuck.
- [ ] 1.3 Paths + spawn point + layout for 9 building plots. **Done when:** clear route spawn → test building.
- [ ] 1.4 Lighting, sky, low-poly materials. **Done when:** consistent clean look, no pink shaders.
- [ ] 1.5 Third-person player prefab. **Done when:** spawns at spawn point.
- [ ] 1.6 Walk + run (Input System). **Done when:** WASD/shift work smoothly on slopes.
- [ ] 1.7 Jump + ground check. **Done when:** jumps and lands reliably.
- [ ] 1.8 Follow camera (Cinemachine). **Done when:** smooth follow, no major clipping.
- [ ] 1.9 Mixamo idle/walk/run/jump animations. **Done when:** animator matches movement.
- [ ] 1.10 One test building. **Done when:** player can walk inside.
- [ ] 1.11 Simple info panel on interact. **Done when:** walking up + key/click shows title + description.
- [ ] 1.12 WebGL player settings (Brotli/Gzip + Decompression Fallback, sizes). **Done when:** WebGL build completes.
- [ ] 1.13 Publish build manually to `gh-pages` branch, enable Pages. **Done when:** public HTTPS URL loads and I can walk around.

## Phase 2 — Reusable building system + content
- [ ] 2.1 `ProjectData` ScriptableObject. **Done when:** has all fields from CLAUDE.md §7.
- [ ] 2.2 `ProjectBuilding` prefab reads `ProjectData`. **Done when:** two buildings show different data from one prefab.
- [ ] 2.3 Enter/interact flow. **Done when:** entering a building opens its presentation.
- [ ] 2.4 Image gallery walls. **Done when:** multiple images display/browse.
- [ ] 2.5 Video screen (URL mode, click-to-play). **Done when:** MP4 from GitHub Pages plays in WebGL build.
- [ ] 2.6 Rotating model pedestal. **Done when:** model appears at correct scale and rotates.
- [ ] 2.7 Optional model animation. **Done when:** flagged projects play their clip.
- [ ] 2.8 Addressables per building. **Done when:** building content loads on approach; initial download not increased.
- [ ] 2.9 Lobby / About Me (photo, skills, contact, resume PDF link).
- [ ] 2.10 BR1 multiplayer game (video + characters).
- [ ] 2.11 AR Pump Assembly Line (Best Paper Award ICMDMSE 2020).
- [ ] 2.12 e-Kanban / ALS with Additive Manufacturing.
- [ ] 2.13 VR scenarios for autistic kids (Embright Infotech).
- [ ] 2.14 VR/AR e-learning PICO / HTC Vive (TalentQuest).
- [ ] 2.15 Point cloud → 3D object (Appville).
- [ ] 2.16 AR ABC phonics + AR dancing avatar.
- [ ] 2.17 Atmospheric Water Generator patent + OSHA safety (Best Project Award).
  **Done when (2.9–2.17):** each building shows its own text, images, video and model in the live build.

## Phase 3 — Multiplayer + paintball (Photon Fusion 2 Shared)
- [ ] 3.1 Install Fusion 2, set App ID in PhotonAppSettings. **Done when:** connects to Photon in WebGL build.
- [ ] 3.2 Shared Mode session join. **Done when:** two browser tabs join the same session.
- [ ] 3.3 Network player spawn. **Done when:** each visitor spawns exactly once.
- [ ] 3.4 Sync movement + animation. **Done when:** each tab sees the other move/animate.
- [ ] 3.5 Name tags. **Done when:** correct name above each remote player.
- [ ] 3.6 Online player count UI. **Done when:** count is correct on join/leave.
- [ ] 3.7 Local paintball raycast + splat. **Done when:** shooting leaves a splat, no damage.
- [ ] 3.8 Sync paintball via RPC. **Done when:** other tab sees the splat.
- [ ] 3.9 Pool/limit splats. **Done when:** spamming doesn't grow object count unbounded.

## Phase 4 — Vivox voice
- [ ] 4.1 Install Vivox + Unity Authentication init. **Done when:** Vivox logs in inside WebGL build.
- [ ] 4.2 Join Voice button → global channel. **Done when:** browser asks mic permission and joins.
- [ ] 4.3 Mute/unmute. **Done when:** toggling stops/starts transmission.
- [ ] 4.4 Speaking indicator (if SDK supports on WebGL). **Done when:** shows, or limitation documented.
- [ ] 4.5 Two-browser voice test. **Done when:** two sessions hear each other.

## Phase 5 — Supabase login, profile, access control
- [ ] 5.1 `SupabaseClient` using UnityWebRequest + ClientConfig. **Done when:** health request succeeds from WebGL.
- [ ] 5.2 Create tables `profiles`, `access_control`, `world_settings` (SQL migration in `Documentation/`). **Done when:** tables exist.
- [ ] 5.3 RLS policies. **Done when:** a user can't read/write another user's profile; clients can't edit access tables.
- [ ] 5.4 Email + 6-digit OTP login. **Done when:** login works in browser; wrong code rejected.
- [ ] 5.5 Profile create/update. **Done when:** profile saved and reloaded on next login.
- [ ] 5.6 Avatar skin selection. **Done when:** chosen skin saved and restored.
- [ ] 5.7 Optional company/role fields. **Done when:** saved and retrieved.
- [ ] 5.8 Profile name → multiplayer name tag. **Done when:** others see my profile name.
- [ ] 5.9 Access gate (is_open + allowlist checked before Photon connect). **Done when:** blocked users see a clear message and can't load the world.
- [ ] 5.9b (Optional hardening) Photon Custom Authentication via Supabase Edge Function. **Done when:** a client skipping the gate is rejected by Photon.
- [ ] 5.10 Open/close world from Supabase dashboard. **Done when:** flipping `is_open` takes effect without rebuild.
- [ ] 5.11 Blocked / closed UI. **Done when:** clear messages for each case.

## Phase 6 — Polish, optimisation, CI, docs
- [ ] 6.1 Polish lobby + loading screens. **Done when:** first-time visitor understands what to do.
- [ ] 6.2 Mobile touch controls. **Done when:** walk/look/interact work on a phone browser.
- [ ] 6.3 Download size audit. **Done when:** initial download < 50 MB (report in Documentation).
- [ ] 6.4 Optimise textures/models/materials. **Done when:** no oversized assets; stable framerate.
- [ ] 6.5 Browser compatibility smoke test (Chrome, Safari, Android Chrome). **Done when:** results recorded.
- [ ] 6.6 GitHub Actions + game-ci build & deploy (Unity license as repo secrets). **Done when:** push to main deploys automatically.
- [ ] 6.7 Full regression (2 browsers: multiplayer + voice + login). **Done when:** all pass on live URL.
- [ ] 6.8 README (architecture, setup, deploy) + `Documentation/LIMITATIONS.md`. **Done when:** a new dev could set it up.

## Future — OpenUSD / Omniverse (do NOT start without approval)
- [ ] F.1 Evaluate Unity USD packages on Unity 6.
- [ ] F.2 Editor-only USD import pipeline.
- [ ] F.3 Export world scene to USD; validate in NVIDIA Omniverse.
- [ ] F.4 OpenUSD / Omniverse portfolio building.
