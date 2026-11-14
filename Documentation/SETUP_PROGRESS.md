# Setup progress (before Phase 0)

Project path: `~/PeronalProjects/UnityProject/PraveensProjectWorld`
Detailed how-to for each step: `Documentation/SETUP_MAC.md`

**Progress: 8 / 16 done**

| # | Step | Who | Status |
|---|---|---|---|
| 1 | Unity project created (6000.3.2f1, URP, Unity Cloud linked) | You | ✅ Done |
| 2 | Project files added (CLAUDE.md, PLAN.md, .gitignore, Config, SourceAssets, Documentation) | Claude | ✅ Done |
| 3 | VS Code + Claude Code extension + Unity extension | You / Claude checks | ✅ Done |
| 4 | Unity → External Script Editor = VS Code | You | ✅ Done |
| 5 | WebGL Build Support module installed for 6000.3.2f1 | You | ✅ Done |
| 6 | GitHub CLI installed + `gh auth login` | You | ✅ Done |
| 7 | `git init` + first commit + GitHub repo created & pushed | You (commands given) | ✅ Done — https://github.com/praveenjjj/praveens-project-world |
| 8 | Claude Code CLI installed + signed in | You | ✅ Done — v2.1.308 (Homebrew), signed in (claude.ai) |
| 9 | Photon Fusion 2 app created, App ID copied | You | ⬜ |
| 10 | Vivox enabled in Unity Cloud project | You | ⬜ |
| 11 | Supabase project created, URL + anon key copied | You | ⬜ |
| 12 | `Config/Local/ProjectSecrets.json` filled | You | ⬜ |
| 13 | Unity MCP connected to Claude Code (`/mcp` shows connected) | You | ⬜ |
| 14 | Supabase MCP connected (read-only first) | You | ⬜ |
| 15 | Source assets + `about.txt` per project in `SourceAssets/` | You (can run in parallel) | ⬜ |
| 16 | Kickoff prompt run → Phase 0 report | You + Claude Code | ⬜ |

## Notes
- Unity Version Control (Plastic) was switched on when the project was created (`.plastic/`, `ignore.conf`). We use **Git**; both are in `.gitignore`.
- Project has URP 17.0.1, Input System 1.16, Unity AI Assistant packages. Phase 0 will check URP version matches the editor.
- `Assets/Testscript.cs` was in the template/project — left untouched.
- GitHub account: **praveenjjj** for now (repo `praveenjjj/praveens-project-world`). Move to **PraveenKumarLean** before sharing with recruiters (`gh repo transfer` or GitHub → Settings → Transfer; Pages URL changes, so update `githubPagesBaseUrl` in secrets).
