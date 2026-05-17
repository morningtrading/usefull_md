agents.md
## Project Overview
trading crypto and stocks using algo.
clean coding- easy maintainable and 100 % tested
## Build & Test
#- Install: `pnpm install`
#- Dev: `pnpm dev`
#- Test: `pnpm test`
#- Lint: `pnpm lint:fix`

## Code Standards

- all parameters are configurable in config file
- all paths are relative
 all files generated (code and data) shall have a prefix with project name before like SCA_ for Scalperbot
- always number every items with a unique key, with increment, like trade_001  or cron_01 or display_01 etc... 
- always run any change through syntax check
- write the code base  modular, avoid large files. separate code in functions.
- build always debugging options. 
- document every line and bloc of code with : objective, rational (why we nhave this line of code?), dependancies,expected output, how to test.
- log execution.
- update readme for every change impacting user / MMI / VDI
- check for dead code and propose deletion or seggregation.
- keep  a configuraiton control in the readme lsiting the tree structure of the code base in a hierarchical tree view.
- think early about bashobard (using streamlite or equivalent) which have tab and display key metrics and health status of the code

## Code style

- **No fake or synthetic data.** Use real data or let the script fail. Silent fallbacks to dummy values hide real problems.
- **Minimal error handling.** Errors should surface, not be swallowed by speculative `try/except`. Wrap only at boundaries you actually understand.
- **No secrets in output.** Never print `.env` contents, API keys, private keys, or credential dumps.
- **Keep files under ~800 lines.** Split into modules when they grow past that; update README/docs to reflect the new layout.
- **Names over comments.** Prefer clear naming; reserve comments for non-obvious *why*, not *what*.

---
- **Question assumptions before coding.** "The first solution that works" is rarely the right one — sketch the architecture before typing.
- **Untested code is speculative.** Confirm you've executed the changed feature and observed results yourself. Type checks and unit tests verify correctness, not feature behavior.
- **Time calculus.** Thirty seconds saved skipping tests typically costs thirty minutes in debugging.
- **Quality gates.** Don't claim "done" without running the thing end-to-end.
### Key principles
1. **Transparency first** — enough context for someone else to evaluate the result.
2. **Reproducibility** — enough detail to reproduce exactly.
3. **Risk awareness** — overfitting risks and limitations called out, not buried.
4. **Comparison enabled** — consistent formatting across runs.

---
- **Run risk checks first.** Before any decision-making agent or signal generator, evaluate portfolio risk, P&L, and exposure.
- **Use circuit breakers.** Hard limits on max loss, max position size, and minimum balance — configurable, not buried in code.
- **Confirm destructive actions.** Closing positions or transferring funds should require an explicit confirmation step (manual or AI-confirmed), not be a silent side effect.



## Development workflow: Explore → Plan → Code → Test

1. **Explore** — map the relevant files first. Use parallel subagents for breadth; return paths and context, not summaries.
2. **Plan** — sketch the implementation approach, test coverage, doc updates. Pause to clarify ambiguities before coding.
3. **Code** — follow established patterns in the repo. Autoformat. Address reasonable linter warnings.
4. **Test** — run the suite; for UX-impacting changes, verify in a browser yourself. Document which scenarios you actually ran.
5. **Document** — PR-ready report: objectives, design decisions with rationale, commands useful for reproducing the work.

---
## Testing Requirements
- All PRs must include tests
- Use vitest for unit tests, playwright for e2e
- safety net applied from the begining on all code items

## Code style preferences. 
-use ES modules, prefer named exports, 2-space indentation.

# Developer Preferences & Local Setup
Developer: [wavegrader]

## Local Endpoints
##- Dev Auth Sandbox: `http://localhost:8080/auth`
##- Test Database Name: `dev_db_local`
##- Test User: `test_user_01@example.com`

## Personal AI Preferences
- never say something works of we have not tested it
- never say something is fixed if not tested
- do not lie, do not flatter
- Tone: Be concise, give brief explanations, do not write long essays.
- Suggestion style: Only provide the changed snippet rather than the entire file.
- When saving draft ideas, place them in the `/scratchpad` directory.
- ask questions of needed, in the form of multiple choice questions
## Environment & dependencies

- **Don't create a new virtual environment if one already exists.** Reuse the project's venv/conda env. Spawning parallel envs causes "works on my machine" drift.
- **Update the lockfile when you add a package.** `pip freeze > requirements.txt`, `poetry lock`, `uv lock` — whichever the repo uses.
- **Don't move files without asking.** Creating new files is fine; relocating existing ones breaks imports, git history, and other agents' assumptions.

---

## Autonomous execution loops

- **Default loop interval should be configurable**, not hardcoded.
- **Agents must continue on error.** A single failing agent shouldn't take down the orchestrator. Log and proceed.
- **Graceful shutdown.** Keyboard interrupt should close positions/connections cleanly, not leave dangling state.
- **Color-coded console logging** (or a structured log format) makes multi-agent output legible.

## Common anti-patterns to avoid

- Hard-coding paths that only work on one machine (`/Users/foo/...`, `C:\\Users\\...`).
- Using retired model IDs from training-data examples without checking the current family.
- Burying risk limits inside agent code instead of surfacing them in config.
- Skipping the metadata header on backtest results "to save space" — that's exactly where the misleading reports come from.
- Adding fallbacks/defaults for failure modes that should be fatal (e.g., missing API key → silently use a stub).


