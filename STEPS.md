# Part 1: Architecture — what was done

The goal: turn a one-line idea ("track my caffeine, remind me during work hours")
into a design the build could follow, without a handoff document between
design and code. Everything happened in one Claude Code session.

## Steps

1. **Set up the project.** Created this folder, checked the tooling on the
   machine (Node 25, npm, git, Docker, Python; no `gh`), and started a git repo.
2. **Wrote the demo runbook** (`docs/DEMO-RUNBOOK.md`): the four parts, the
   prompts to use live, what to show the audience, and a git tag per part so a
   failed live step can be recovered.
3. **Drafted the architecture** (`docs/ARCHITECTURE.md`): requirements, decisions
   with alternatives, system diagram, data model, API and reminder rules. The
   first draft was a Docker container with an API, SQLite and web push.
4. **Wrote `CLAUDE.md`**, the project memory every later session reads.
5. **Moved the architecture onto a Claude Design canvas**: a system diagram, the
   reminder-rule flowchart and the key decisions, drawn from the same session.
   The canvas and the doc stay in step; one is linked from the other.
6. **Changed course on cost.** The goal was "as free as possible" and personal
   use, so the design became browser-only: a static app on Cloudflare Pages,
   data in the browser, reminders from the open tab. Docker, the API and the
   database were removed from the canvas and the docs together.
7. **Added the user's requirements:** custom reminder times (two modes: every N
   hours, or at set times), work hours in a chosen time zone, drink search with
   a built-in list, and custom drinks with their own caffeine amount.
8. **Designed the screens on the canvas:** Today, Settings and Calendar
   mock-ups, in a terminal ("hacker") theme with light and dark modes, each a
   working prototype with a theme toggle.
9. **Designed the coffee cup:** a pixel-style cup that fills as caffeine is
   logged, steams, turns amber at the limit and overflows past it. Then the
   Today layout: cup and metrics on the left, a collapsible history drawer on
   the right, and an add-drink popup.
10. **Added the calendar:** one month at a time, three colour levels (none,
    some, over the limit) with the percentage of the daily limit on each day.
11. **Added the storage interface:** an async `CaffeineStore` with a
    localStorage version for v1 and an `HttpStore` as a later swap, so a
    database can replace the browser without changing the screens.
12. **Committed and tagged** `part-1-architecture`. This folder is frozen; the
    build repos carry a living copy of the architecture doc.

## Outputs

- `docs/ARCHITECTURE.md`, `docs/DEMO-RUNBOOK.md`, `CLAUDE.md`
- The design canvas: https://claude.ai/artifact/BTrzarsxNJSB65EYwf9kBz
- Tag `part-1-architecture`

## Worth showing live

- Plan mode: the design is reviewed before anything is written.
- Changing your mind mid-design (Docker to browser-only) and watching the
  canvas and the docs update together.
- `CLAUDE.md` as the memory later sessions read without being told.
