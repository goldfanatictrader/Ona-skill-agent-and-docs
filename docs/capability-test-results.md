# Ona Capability Test Results

All tests run against goldfanatictrader/Ona-test via ona ai automation (Ona CLI) using isolated automation environments.

## Model / Effort smoke tests

| Test Name | Model | Effort | Steps | Verified Output |
|---|---|---|---|---|
| am-terra | GPT_5_6_TERRA | MEDIUM | task > agent > report(command) | TERRA OK |
| am-luna | GPT_5_6_LUNA | LOW | task > agent > report(command) | LUNA OK |
| am-effort | GPT_5_6_SOL | EXTRA_HIGH | task > agent > report(command) | EXTRA_HIGH OK |

## Report step type tests

| Key | Type | Command | Verified Value |
|---|---|---|---|
| raw | string | cat test.log | 3 failed / 42 passed |
| passed | integer | cat int.log | 42 |
| coverage | float | cat float.log | 3.14 |
| green | boolean | cat bool.log | true |

## SCM tool test

| Action | Result | Evidence |
|---|---|---|
| Create GitHub issue via agent | success | Issue #2 on goldfanatictrader/Ona-test titled "Capability test: issue creation" (confirmed via GitHub API) |

## Planning-only test

| Action | Result | Evidence |
|---|---|---|
| Agent writes detailed PLAN.md without modifying code | success | Report captured 200+ line plan; no code changes |

## Notes

- Model choice: SOL is the largest/most capable of the 5.6 trio; TERRA is balanced; LUNA is lightweight/fast.
- All tests used codexSettings in automation YAML to select model + effort.
- GPT_6_Astra is the highest capability model but is not currently enabled for the test organization.
