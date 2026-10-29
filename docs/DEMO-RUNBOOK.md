# Demo runbook: building an app with Claude Code

The app is **Caffeine Tracker**: you log caffeine intake, and if you go too long
without caffeine during your work hours, you get a reminder.

The demo has four parts. Each part ends with something visible on screen and a
git commit, so you can jump to any part by checking out its tag.

| Part | Theme | What Claude Code does | What the audience sees | Git tag |
|---|---|---|---|---|
| 1 | Architecture | Turns a one-line idea into requirements, decisions and a diagram | `docs/ARCHITECTURE.md`, `CLAUDE.md` | `part-1-architecture` |
| 2 | Application development | Scaffolds and builds the UI, storage and reminder timer | App running locally; logging a drink; a reminder firing | `part-2-app` |
| 3 | Testing | Writes unit and end-to-end tests, then finds and fixes a bug | Green test run; Playwright driving the browser | `part-3-tests` |
| 4 | Production grade | CI, security review, free deploy to Cloudflare Pages | Live pages.dev URL; CI pipeline; `/security-review` output | `part-4-prod` |

## Part 1: Architecture (about 10 min)

Prompt to use live:

> I want an app that tracks my caffeine intake and reminds me if I haven't had
> caffeine during my work hours. Help me design it before we write any code.

Things to show:
- Claude asks clarifying questions or states its assumptions instead of guessing.
- Plan mode: the plan is reviewed before anything is written.
- The output is a real file in the repo (`docs/ARCHITECTURE.md`), not chat text.
- The same design as a Claude Design canvas, drawn from the same session, with no handoff document.
- Changing your mind mid-design: we moved from Docker to browser-only because the
  goal was "free". Show Claude updating the canvas and the docs together.
- `CLAUDE.md`: the project's memory, read by every later session.

## Part 2: Application development (about 20 min)

Prompts to use live:

> Scaffold the project as described in docs/ARCHITECTURE.md.

> Build the "log a drink" flow end to end.

> Add the reminder timer and browser notifications.

Things to show:
- Claude reads `CLAUDE.md` and the architecture doc without being told to.
- Parallel work: one session builds `packages/core`, another builds the UI.
- The in-app browser previewing the running app.
- Trigger a reminder with `?demo=1` (see "Demo mode" in the architecture doc).

## Part 3: Testing (about 15 min)

Prompts to use live:

> Write tests for the reminder rules. Cover the edge cases.

> Add a Playwright test for logging a drink.

Things to show:
- Claude finds edge cases on its own: midnight, weekends, time zones, daily limit.
- Plant a bug beforehand (for example, an off-by-one in the work-hours check),
  then let the tests catch it and have Claude fix it.
- `/code-review` on the branch.

## Part 4: Production grade (about 15 min)

Prompts to use live:

> Make this production ready: CI that runs the tests, security headers, and a
> free deploy to Cloudflare Pages.

Things to show:
- `/security-review`
- A GitHub Actions pipeline running the tests on every push.
- Cloudflare Pages deploying from GitHub, then opening the live pages.dev URL.
- Before the demo: install `gh` and sign in, and create a free Cloudflare account.

## Rehearsal checklist

- [ ] Do a full dry run and tag each part.
- [ ] Keep the tags, so if a live step fails you can `git checkout part-N-*` and carry on.
- [ ] Allow browser notifications in the demo browser in advance.
- [ ] Open the app with `?demo=1` so a reminder fires on stage.
- [ ] Turn off Do Not Disturb / Focus mode, or notifications won't appear.
