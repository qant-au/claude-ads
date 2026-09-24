# Claude Ads Repository Instructions

@AGENTS.md

`AGENTS.md` is the canonical portable repository contract. `ads/SKILL.md` is
the product entrypoint. Load focused skills and references only when the task
routes to them.

## Architecture

- `ads/`: primary `/ads` orchestration skill and shared references.
- `skills/`: focused platform and workflow skills.
- `agents/`: bounded workers that return results to the conductor.
- `claude_ads_core/`: deterministic schemas, normalization, scoring, reporting,
  and adapter contracts.
- `control-plane/`: product boundaries, evidence and capability manifests,
  safety policy, maturity, ecosystem decisions, and release gates.
- `tests/` and `evals/`: deterministic and model-facing verification.

## Development

- Keep skill entrypoints concise and use progressive disclosure.
- Keep platform facts and volatile guidance in dated references, not permanent
  root instructions.
- Python tools expose a CLI, structured output, and tests proportional to risk.
- Agents return schema-valid results; the conductor owns final artifacts.
- Use manifest-derived counts and capability status instead of hand-maintained
  claims.

## Verification

Run the focused tests for the changed surface, then the complete local suite.
Release claims additionally require every gate in
`control-plane/RELEASE_REQUIREMENTS.md` and required remote CI.

## Port registry

Every host port used anywhere under `/Users/adam/Projects` — **including this project's** — is recorded in one complete source of truth: [`/Users/adam/Projects/claude-skills-shared/PORTS.md`](/Users/adam/Projects/claude-skills-shared/PORTS.md).

- **Need a port (new or changed)?** Open `PORTS.md`, find this project's reserved range in the legend, and take the lowest unused port in that range.
- **After** adding/changing/removing any port binding (`docker-compose ports:`, `restart.sh`, dev `--port`): add/update the row in `PORTS.md` **in the same commit**.
- **Validate:** `python3 /Users/adam/Projects/claude-skills-shared/scripts/check-ports.py` (errors on unregistered ports and collisions).
