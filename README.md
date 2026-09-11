# Ona Skill Agent & Docs

Repository of tested Ona / Codex agent capabilities, test results, and reusable Ona skill definitions.

## Contents

| Path | Purpose |
|---|---|
| docs/capability-test-results.md | Empirical results of capability test battery |
| docs/how-tests-were-run.md | Automation YAML snippets used to run the tests |
| skills/ona-smart-runner.md | Reusable Ona skill definition for running Codex tasks |
| AGENTS.md | Agent instructions for working in this repo |

## Test summary

| Model | Effort | Capability Tested | Result |
|---|---|---|---|
| GPT_5_6_TERRA | MEDIUM | Model loads and runs | OK |
| GPT_5_6_LUNA | LOW | Model loads and runs | OK |
| GPT_5_6_SOL | EXTRA_HIGH | High effort reasoning | OK |
| GPT_5_6_SOL | MEDIUM | Report step (string/int/float/bool) | OK |
| GPT_5_6_SOL | HIGH | SCM tool - GitHub issue creation | OK |
| GPT_5_6_SOL | HIGH | Planning only (no code changes) | OK |

Tests performed by automated ona ai automation runs on 11 Sep 2026.
