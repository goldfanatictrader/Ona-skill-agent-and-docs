---
name: Ona Codex Smart Runner
description: Execute a Codex agent task with automatically selected model and effort based on job complexity.
slash_command: /run-codex
---

# Ona Codex Smart Runner Skill

Use this skill to run a Codex agent task against a repository. The skill automatically selects the most appropriate GPT-5.6 model variant and reasoning effort based on the described complexity of the job.

## Prerequisites

### Check Ona CLI installation

Before anything else, verify that the Ona CLI is installed:

  command -v ona

If the command is not found, display the following message and stop:

  Ona CLI is not installed. Install it with:
    curl -fsSL https://ona.com/install.sh | sh

After installation, verify with:

  ona --version

### Check authentication

Run:

  ona whoami

If it fails or shows no logged-in user, output:

  Please log in first: ona login

and stop. In automated contexts where credentials are already configured, skip this check.

## Inputs

| Input | Required | Description |
|---|---|---|
| repo_url | Yes | GitHub repository URL (e.g. https://github.com/owner/repo) |
| task_description | Yes | What you want the agent to do (one or more sentences) |
| environment_class_id | Yes | Ona environment class ID (e.g. 019f6ebd-13d5-7730-bef9-3fefa61551d5 for Small) |
| create_pr | No | true (default) to open a PR with the changes; false to just run in the environment |

## Steps

1. Classify task complexity using these heuristics:
   - Low: single-file edit, rename, documentation, minor bug fix, less than 50 lines changed.
   - Medium: new feature in 1-3 files, moderate logic, tests required, 50-300 lines.
   - High: multi-file refactor, architecture changes, deep reasoning, security-sensitive, more than 300 lines.

2. Choose model and effort:

   | Complexity | Model | Reasoning Effort |
   |---|---|---|
   | Low | CODEX_OPEN_AI_MODEL_GPT_5_6_LUNA | CODEX_REASONING_EFFORT_LOW |
   | Medium | CODEX_OPEN_AI_MODEL_GPT_5_6_TERRA | CODEX_REASONING_EFFORT_MEDIUM |
   | High | CODEX_OPEN_AI_MODEL_GPT_5_6_SOL | CODEX_REASONING_EFFORT_ULTRA |

3. Generate automation YAML with:
   - codexSettings using the selected model and effort.
   - One agent step whose prompt is the task_description.
   - If create_pr is true, add a pullRequest step with a branch name derived from a short slug of the task (e.g. ona/auto-<slug>). Otherwise omit the pullRequest step.
   - Use limits: { maxParallel: 1, maxTotal: 1 }.
   - Target repositoryUrls.repoUrls: [repo_url] and set environmentClassId to the provided value.

4. Run the automation:

   ona ai automation create <yaml>
   ona ai automation start <id> --wait
   ona ai automation executions outputs <execution-id> -o json
   ona ai automation delete <id>

5. Report results: PR URL (if created), execution ID, and key outputs.
