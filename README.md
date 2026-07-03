
# NocturnX — Privacy Patch Automator 🛡️✨

A tiny Python tool to apply modern privacy tweaks to Windows, macOS, and Linux. Review, dry-run, and then apply patches safely.

Why use this? 💡
- Automate repeatable privacy hardening steps
- Reviewable dry-run output and backups
- Easy to extend for your organization

Quick start 🚀

1. Create a venv and activate it.

Windows (PowerShell):
```powershell
python -m venv venv
venv\Scripts\Activate.ps1
```
macOS / Linux:
```bash
python -m venv venv
source venv/bin/activate
```

2. Install deps (if present):
```bash
pip install -r requirements.txt
```

Run (preview then apply) ✅

- Dry-run Windows:
```powershell
python main.py --os windows --dry-run
```
- Apply Windows (Admin):
```powershell
python main.py --os windows --apply
```
- Dry-run macOS:
```bash
python main.py --os macos --dry-run
```
- Apply macOS (sudo):
```bash
sudo python main.py --os macos --apply
```
- Dry-run Linux:
```bash
python main.py --os linux --dry-run
```
- Apply Linux (sudo):
```bash
sudo python main.py --os linux --apply
```

Recommended flags:
- `--dry-run` (preview) · `--apply` (execute) · `--backup` · `--log FILE` · `--yes` (non-interactive)

Safety first ⚠️
- Always run `--dry-run` and test in a VM.
- Keep backups and provide rollback steps.
- Run with proper privileges only when ready.

Contributing & notes 📝
- Add OS-specific patch functions to `main.py` and document each change.
- Add `requirements.txt` for external packages you use.
- Include tests and a rollback plan in PRs.

License
- No license included — add `LICENSE` if you want to open-source.

Questions or help? Open an issue or PR. 🙌


