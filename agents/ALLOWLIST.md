# Agent Command Allowlist

This file defines recommended command prefixes to pre-approve for agent execution in this repo.

## Core GitHub Operations (Recommended)
- `["gh", "repo", "view"]`
- `["gh", "run", "list"]`
- `["gh", "run", "watch"]`
- `["gh", "pr", "create"]`
- `["gh", "pr", "view"]`
- `["gh", "pr", "checks"]`

## Core Git Operations (Recommended)
- `["git", "status"]`
- `["git", "add"]`
- `["git", "commit"]`
- `["git", "push"]`
- `["git", "fetch"]`
- `["git", "log"]`
- `["git", "diff"]`

## Project Test/Build Operations (Recommended)
- `["make", "test-mamba"]`
- `["make", "test-venv"]`
- `["make", "gh-status"]`
- `["make", "gh-ci"]`
- `["bash", "scripts/test_shared_control.sh"]`
- `["bash", "scripts/setup_venv.sh"]`

## Suggested Optional Entries
- `["python", "-m", "pytest"]`
- `["python", "-m", "pip", "install"]`
- `["mamba", "run", "-n", "shared-control", "python", "-m", "pytest"]`
- `["mamba", "run", "-n", "shared-control", "python", "-m", "pip"]`

## Safety Notes
- Do not pre-approve destructive prefixes (`rm`, `git reset --hard`, force-push patterns).
- Prefer narrow prefixes over broad ones.

