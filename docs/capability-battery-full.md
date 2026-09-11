# Ona capability battery — full results
## Model selection (by complexity)
| Complexity | Model |
|---|---|
| Low | CODEX_OPEN_AI_MODEL_GPT_5_6_LUNA |
| Medium | CODEX_OPEN_AI_MODEL_GPT_5_6_TERRA |
| High | CODEX_OPEN_AI_MODEL_GPT_5_6_SOL |
## Reasoning effort
| Effort | CODEX_REASONING_EFFORT_LOW / MEDIUM / ULTRA |
## Report output types (all pass)
string, integer, boolean, float
## Acceptance criteria
- threshold `< 40` → FAIL
- `score >= 40` → PASS (battery: 45)
## Multi-repository trigger (passes)
- two repositories in one automation
