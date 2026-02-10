# Agent Rules

See `agents/ALLOWLIST.md` for the repo command-prefix allowlist used to speed up GitHub and CI operations.

## Python Environment
- Default to the local virtual environment named `.venv-hil-pusht` at repo root.
- If local venv dependency installation is blocked, use the `shared-control` mamba environment.
- Do not install dependencies globally.
- Do not run tests or scripts with the system Python.

## Setup Workflow
1. Create/update the venv:
   - `bash scripts/setup_venv.sh`
2. Activate it:
   - `source .venv-hil-pusht/bin/activate`
3. Verify interpreter:
   - `python -c "import sys; print(sys.prefix)"`
   - Expected output includes `.venv-hil-pusht`.

## Mamba Fallback Workflow
1. Install this repo into `shared-control`:
   - `mamba run -n shared-control python -m pip install -e . --no-deps`
2. Run tests in `shared-control`:
   - `mamba run -n shared-control python -m pytest -q`
3. One-command helper:
   - `bash scripts/test_shared_control.sh`

## Command Conventions
- Run package and test commands from repo root.
- Preferred local-venv commands:
  - `python -m pip install -e .[dev]`
  - `python -m pytest -q`
- Fallback mamba commands:
  - `mamba run -n shared-control python -m pip install -e . --no-deps`
  - `mamba run -n shared-control python -m pytest -q`
- Make targets:
  - `make setup-venv`
  - `make test-venv`
  - `make test-mamba`

## GitHub Operations
- Use `git` + `gh` directly from this repo; do not rely on manual website-only steps.
- Standard branch flow:
  1. `git checkout -b <feature-branch>`
  2. implement + test
  3. `git add -A && git commit -m "<message>"`
  4. `git push -u origin <feature-branch>`
  5. `gh pr create --fill`
- Standard mainline update flow (when instructed to ship directly):
  1. run tests (`make test-mamba` or local venv equivalent)
  2. `git add -A && git commit -m "<message>"`
  3. `git push origin main`
- CI and run status checks:
  - `make gh-status`
  - `make gh-ci`
- If `gh` API access is unavailable in a restricted environment, still push via `git` and treat GitHub Actions on the remote as the source of truth for pass/fail.
- Resolve CI failures before declaring work complete.
