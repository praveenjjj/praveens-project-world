# Setup checklist (macOS, Apple Silicon)

Already done: Unity 6 (6000.3.2f1), Git, Node, Python, uv · Unity project created · these files added.

## 1. Tools (Terminal)
- [ ] Homebrew (if missing): see https://brew.sh
- [ ] GitHub CLI: `brew install gh` → `gh auth login` (GitHub.com → HTTPS → login with browser)
- [ ] Claude Code: install from https://code.claude.com/docs (native installer or npm), then run `claude` once and sign in
- [ ] VS Code extensions: **Claude Code**, **Unity** (Microsoft)
- [ ] Unity: Edit → Preferences → External Tools → External Script Editor = Visual Studio Code
- [ ] Unity Hub → Installs → 6000.3.2f1 → Add modules → **WebGL Build Support** (if not installed)

## 2. GitHub repo
From the project folder in Terminal:
```bash
cd ~/PeronalProjects/UnityProject/PraveensProjectWorld
git init -b main
git add .
git commit -m "Initial Unity 6 URP project + Claude Code rules and plan"
gh repo create praveens-project-world --public --source=. --push
```
(GitHub Pages gets enabled in task 1.13 — Claude will do it with your approval.)

## 3. Service accounts (you sign in; Claude never handles passwords)
- [ ] **Photon:** https://dashboard.photonengine.com → Create new app → type **Fusion** (Fusion 2) → copy App ID
- [ ] **Unity Cloud / Vivox:** https://cloud.unity.com → your project (the one this Unity project is linked to) → Products → **Vivox** → enable. In Unity: Edit → Project Settings → Services → confirm the project is linked.
- [ ] **Supabase:** https://supabase.com → New project (region: Mumbai/Singapore) → Project Settings → API → copy **Project URL** and **anon/publishable key**. ⚠️ Never copy the service_role key anywhere in this project.

## 4. Put the values in the local secrets file
```bash
cp Config/ProjectSecrets.example.json Config/Local/ProjectSecrets.json
open -e Config/Local/ProjectSecrets.json   # paste your values
git check-ignore -v Config/Local/ProjectSecrets.json   # must print a match
```

## 5. MCP servers for Claude Code (project scope → saved in .mcp.json)
Pick **one** Unity MCP:
- **Unity CLI (official):** follow Unity's "Unity CLI / unity mcp" docs → `unity mcp configure claude`
- **or CoplayDev "MCP for Unity":** Unity → Package Manager → Add from git URL (see https://github.com/CoplayDev/unity-mcp) → Window → MCP for Unity → Auto-setup for Claude Code

Supabase MCP: follow https://supabase.com/docs/guides/getting-started/mcp — add it with project scope and read-only mode first.

Check: run `claude` in the project folder → type `/mcp` → both servers show **connected**.
Commit `.mcp.json` only if it contains no keys or tokens.

## 6. Assets
Drop original files into `SourceAssets/<Project>/` (models, images, MP4s, resume PDF, photo).
Also write 2–3 lines per project in `SourceAssets/<Project>/about.txt`.

## 7. Start
```bash
cd ~/PeronalProjects/UnityProject/PraveensProjectWorld
claude
```
`/model opusplan` → Shift+Tab (Plan Mode) → paste the KICKOFF PROMPT from `Documentation/PROMPTS.md`.
