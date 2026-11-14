# Prompts for Claude Code

Before pasting: run `claude` in the project folder (or open the Claude Code panel in VS Code),
type `/model opusplan`, then press **Shift+Tab** until Plan Mode is on.

---

## KICKOFF PROMPT (first session only)

```
Read CLAUDE.md and PLAN.md completely. They are the source of truth.

Do Phase 0 only. This is READ-ONLY: do not install packages, change settings,
create/modify files or commit anything.

1. Unity project: editor version, URP active, WebGL build support, existing scenes,
   packages, console errors (use the Unity MCP).
2. Tools: git status + remote, `gh auth status`, Unity MCP tools available,
   Supabase MCP tools available, any browser-testing tool.
3. Services: Photon Fusion App ID, Unity Cloud project link (for Vivox), Supabase project,
   GitHub repo/Pages — check presence only, never print keys.
4. Folder structure vs CLAUDE.md §4 and .gitignore coverage.
5. Compatibility audit (check current docs): Fusion 2 Shared + WebGL,
   Vivox + WebGL, Supabase via UnityWebRequest + email OTP, Addressables on GitHub Pages.

Report in sections: A) Environment status (PASS / FAIL / NOT CONFIGURED / NEEDS MANUAL CHECK),
B) Unity project, C) MCP status, D) Services, E) Compatibility risks,
F) Checklist of things I must fix manually, G) Which Phase 0 boxes can be ticked.

Then propose a plan for Phase 1 (tasks 1.1–1.13): for each task what you'll create,
files/assets involved, how you'll test it, and the commit message.

STOP and wait for my approval before doing anything else.
```

---

## CONTINUE PROMPT (every later session)

```
Read CLAUDE.md and PLAN.md. Check git status and the Unity project state.
Find the next unchecked, unblocked task in PLAN.md.
Plan it (files, approach, Done-when test) and wait for my approval.
After approval: implement only that task, run its test, report changed files and results,
commit with a clear message, tick the box in PLAN.md, then stop.
If blocked, write the blocker in PLAN.md and propose the smallest fix.
```

---

## STUCK-BUG PROMPT

```
This bug survived 2 attempts. Stop patching. Re-read the relevant scripts and logs,
list 3 possible root causes with evidence for each, propose how to confirm the most
likely one, and wait for my approval.
```
(If still stuck, switch with `/model opus` — or Fable if your plan has it — for that one bug, then back to `/model opusplan`.)
