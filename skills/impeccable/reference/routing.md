# Command guidance

## Workflow questions

Give advice without executing commands; the menu below is only for bare invocations. Consult relevant command references as needed for prerequisites and scope. Link to the [docs](https://impeccable.style/docs/) for the broader workflow guide. If the user also requests execution, follow that request.

## No-argument routing: the context-aware menu

Read this when the user invokes `$impeccable` with no argument. They are asking "what should I do?" Make the menu context-aware instead of static.

Read the project context for this menu. If the launcher is unavailable, suggest the relevant commands from existing project files and the index below. If `impeccable context` reported `NO_PRODUCT_MD`, the project has no captured context yet: lead the menu with `$impeccable init` as the top recommendation (one line on why) and still show the rest below; don't silently jump into init. Otherwise run `.agents/skills/impeccable/scripts/impeccable signals` once and read its JSON, then lead with the **2-3 highest-value next commands**, each with a one-line reason pulled from the signals, followed by the full menu (the [command index](#command-index), grouped by category). **Never auto-run a command; the recommendation is a suggestion the user confirms.**

Reason over the signals; there is no score to obey:

- `setup.hasDesign` false while `setup.hasCode` true → `document` (capture the visual system).
- `critique.latest` is `null` → the project has never been critiqued; for a set-up project with a real surface, offering `$impeccable critique <surface>` is a strong default.
- `critique.latest` with a low `score` or non-zero `p0` / `p1` → `polish` (it reads that snapshot as its backlog and closes it when stale or cleared).
- `git.changedFiles` pointing at one surface → scope `audit` or `polish` to those files specifically, naming them.
- `devServer.running` true → `live` is available for in-browser iteration, and `generate` for one-shot variant runs on a named element; if false, don't lead with either. **`live`, `generate`, and the bundled `impeccable detect` are web-only.** If `setup.platform` is `ios`, `android`, or `adaptive`, don't lead with any of them; the browser overlay and the HTML rule engine don't apply to native app code.
- Otherwise group by intent (build new / improve what's there / iterate visually), tailored to the current surface and `setup.platform`.

**If `scan.targets` is non-empty and `setup.platform` is not `ios`/`android`/`adaptive`, run `.agents/skills/impeccable/scripts/impeccable detect --json <scan.targets joined by spaces>` once** (the bundled detector over local files: no network, no npx; it reads HTML/CSS, so skip it for native projects). `scan.via` tells you what they are: `git-changes` (the markup/style files in your dirty tree, the most relevant set), `source-dir` (e.g. `src`, `app`), `html`, or `root`. Fold the hits into your picks: many quality / contrast hits → `audit` or `polish`; a specific slop family → the matching command (gradient text or eyebrows → `quieter` / `typeset`, flat or gray palette → `colorize`, and so on). It's a real, current signal that beats guessing. If detect errors or the tree is large and slow, skip it and recommend the user run `audit` themselves; never block the suggestion on it.

Keep it to 2-3 pointed picks with the exact command to type. The menu stays the fallback; the recommendation is the lede.

## Command index

| Command | Category | Description | Reference |
|---|---|---|---|
| `craft [feature]` | Build | Deprecated alias for an ordinary new-work request | [reference/craft.md](craft.md) |
| `shape [feature]` | Build | Plan UX/UI before writing code | [reference/shape.md](shape.md) |
| `init` | Build | Capture durable product context in PRODUCT.md | [reference/init.md](init.md) |
| `document` | Build | Generate DESIGN.md from existing project code | [reference/document.md](document.md) |
| `extract [target]` | Build | Pull reusable tokens and components into design system | [reference/extract.md](extract.md) |
| `critique [target]` | Evaluate | UX design review with heuristic scoring | [reference/critique.md](critique.md) |
| `audit [target]` | Evaluate | Technical quality checks (a11y, perf, responsive) | [reference/audit.md](audit.md) · native: [reference/audit.native.md](audit.native.md) |
| `polish [target]` | Refine | Final quality pass before shipping | [reference/polish.md](polish.md) |
| `bolder [target]` | Refine | Amplify safe or bland designs | [reference/bolder.md](bolder.md) |
| `quieter [target]` | Refine | Tone down aggressive or overstimulating designs | [reference/quieter.md](quieter.md) |
| `distill [target]` | Refine | Strip to essence, remove complexity | [reference/distill.md](distill.md) |
| `harden [target]` | Refine | Production-ready: errors, i18n, edge cases | [reference/harden.md](harden.md) |
| `onboard [target]` | Refine | Design first-run flows, empty states, activation | [reference/onboard.md](onboard.md) |
| `animate [target]` | Enhance | Add purposeful animations and motion | [reference/animate.md](animate.md) |
| `colorize [target]` | Enhance | Add strategic color to monochromatic UIs | [reference/colorize.md](colorize.md) |
| `typeset [target]` | Enhance | Improve typography hierarchy and fonts | [reference/typeset.md](typeset.md) |
| `layout [target]` | Enhance | Fix spacing, rhythm, and visual hierarchy | [reference/layout.md](layout.md) |
| `delight [target]` | Enhance | Add personality and memorable touches | [reference/delight.md](delight.md) |
| `overdrive [target]` | Enhance | Push past conventional limits | [reference/overdrive.md](overdrive.md) |
| `clarify [target]` | Fix | Improve UX copy, labels, and error messages | [reference/clarify.md](clarify.md) |
| `adapt [target]` | Fix | Adapt for different devices and screen sizes | [reference/adapt.md](adapt.md) · native: [reference/adapt.native.md](adapt.native.md) |
| `optimize [target]` | Fix | Diagnose and fix UI performance | [reference/optimize.md](optimize.md) |
| `live` | Iterate | Visual variant mode: pick elements in the browser, iterate on alternatives | [reference/live.md](live.md) |
| `generate [n] [action] [element]` | Iterate | Variants, versions, or alternatives of a named element to choose from in the live browser; no manual picking | [reference/generate.md](generate.md) |

`teach` is an alias for `init`. `craft` is a deprecated alias for new visual work.

- **Pin or unpin a shortcut:** When requested, run `<skill-base-dir>/scripts/impeccable pin <pin|unpin> <command>` from the project. Report the result.
- **Manage hooks:** Follow [hooks](hooks.md) for an explicit `$impeccable hooks` request.
- **Inspect or repair setup drift:** Follow [doctor](doctor.md) for an explicit request or an observed context warning. Report the drift and repair only within the user's request.
