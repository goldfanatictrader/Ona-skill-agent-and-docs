# How the capability tests were run

Tests were executed using the Ona CLI ona ai automation commands (create > start --wait > executions outputs > delete). Each automation defined its model/effort in codexSettings and targeted goldfanatictrader/Ona-test as the repository context.

## Automation YAML structure (common parts)

name: <test-name>
agentId: 00000000-0000-0000-0000-000000007800
codexSettings:
  model: CODEX_OPEN_AI_MODEL_GPT_5_6_SOL
  reasoningEffort: CODEX_REASONING_EFFORT_HIGH
triggers:
  - context:
      repositories:
        environmentClassId: 019f6ebd-13d5-7730-bef9-3fefa61551d5
        repositoryUrls:
          repoUrls:
            - https://github.com/goldfanatictrader/Ona-test
    manual: {}
action:
  limits:
    maxParallel: 1
    maxTotal: 1
  steps:
    - task:
        command: "..."
    - agent:
        prompt: "..."
    - report:
        outputs:
          - key: result
            title: Result
            string: {}
            command: "cat result.txt"

## Commands used

ona ai automation create <yaml-file>
ona ai automation start <automation-id> --wait
ona ai automation executions list --automation-id <id> -o json
ona ai automation executions outputs <execution-id> -o json
ona ai automation delete <automation-id>

## Tips

- codexSettings must be at the top level of the YAML (not inside action).
- agentId is required for Codex agent; without it the deprecated Ona agent is used (currently disabled).
- The environment class 019f6ebd-13d5-7730-bef9-3fefa61551d5 (Small) is required for manual triggers.
- Use string: {}, integer: {}, float: {}, boolean: {} in report outputs; exactly one schema field per output.
