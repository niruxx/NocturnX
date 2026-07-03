
# NocturnX — Privacy Patch Automator

NocturnX is a lightweight Python utility that automates recommended privacy hardening steps for modern Windows, macOS, and Linux systems. It provides a structured, auditable approach to applying configuration changes and mitigations (for example: telemetry reductions, optional service tweaks, hosts entries, and privacy-focused settings) in a repeatable way.

This repository is a starting point — `main.py` contains the entrypoint and should be extended with the exact OS patches you want to apply.

**Important:** this tool makes system configuration changes. Always review changes, run in `--dry-run` mode first, and test in a VM before applying to production systems.

## What it does

- Automates a curated set of privacy-related configuration changes per OS.
- Supports dry-run output so you can review planned changes before applying them.
- Produces logs and optional backups of modified files/configs.

## Requirements

- Python 3.10 or newer
- Administrative privileges when applying changes (Windows: run PowerShell as Administrator; macOS/Linux: run with `sudo` or an elevated account)
- Optional: a `requirements.txt` file if additional packages are used (e.g., `pyyaml`, `click`).

If your repository does not include `requirements.txt`, create one with the packages your implementation needs and then run the install step below.

## Installation

Create and activate a virtual environment, then install dependencies:

Windows (PowerShell):

```powershell
python -m venv venv
venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

macOS / Linux:

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

If you don't have any external dependencies yet, you can omit the `pip install` step.

## Running the program

The entrypoint is [main.py](main.py). The recommended workflow is to preview changes with `--dry-run` and then apply them.

Examples (replace `python` with the full path to your venv python if needed):

Dry-run for Windows (run PowerShell as Administrator):

```powershell
python main.py --os windows --dry-run
```

Apply changes to Windows (Administrator required):

```powershell
python main.py --os windows --apply
```

Dry-run for macOS:

```bash
python main.py --os macos --dry-run
```

Apply changes to macOS (use `sudo` if needed):

```bash
sudo python main.py --os macos --apply
```

Dry-run for Linux:

```bash
python main.py --os linux --dry-run
```

Apply changes to Linux (typically requires `sudo`):

```bash
sudo python main.py --os linux --apply
```

Suggested CLI flags (if you implement them in `main.py`):

- `--os <windows|macos|linux>`: select target OS
- `--dry-run`: show planned changes without applying
- `--apply`: apply the changes
- `--backup`: save backups of files before modifying
- `--yes`: non-interactive apply (use with caution)
- `--log FILE`: write operation logs to `FILE`

If `main.py` does not yet support these flags, add them using `argparse` or a CLI library like `click`.

## Safety, auditing, and best practices

- Always run `--dry-run` first and review the output.
- Test in a disposable VM or test lab before applying to production devices.
- Keep backups of changed files and include a way to rollback changes.
- Log every operation and include timestamps and user/host context.
- Prefer minimally invasive changes and provide clear documentation of what each patch does.
- Consider adding a verbose mode and an approval step for dangerous actions.

## Example workflow

1. Create a branch and implement OS-specific patch functions in `main.py`.
2. Run `python main.py --os linux --dry-run` and inspect output.
3. Run `python main.py --os linux --backup --apply` on a test VM.
4. If everything looks good, open a PR with tests and documentation for the changes.

## Adding dependencies

When adding third-party packages, pin them in `requirements.txt`:

```
pyyaml==6.0
click==8.1.3
```

Install them with:

```bash
pip install -r requirements.txt
```

## Contributing

Contributions are welcome. Please include:

- A clear description of the patch and why it improves privacy
- A test or repro showing the change works on the target OS
- A rollback plan or instructions to undo the change

Suggested workflow:

1. Fork the repo and create a feature branch.
2. Add or update `main.py` with focused changes and a test harness.
3. Update `requirements.txt` if you add dependencies.
4. Open a PR and request review.

## Legal & ethical notice

This project modifies system settings. Ensure you have permission to change the devices you run this on. The authors are not responsible for misuse or damage caused by applying these patches. Some changes may affect system telemetry or remote management—verify compliance with organizational and legal requirements before applying.

## Next steps (suggested)

- Add a `requirements.txt` listing runtime dependencies.
- Implement and document CLI flags in `main.py` (dry-run, apply, backup, log).
- Add unit and integration tests (consider using Vagrant/VMs or containers for reproducible test environments).
- Add a `LICENSE` file if you intend to open-source this work.

## Contact

Open an issue or PR on GitHub for questions or collaboration.

