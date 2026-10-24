## Project Overview

- **Project Name:** Meeting Assistant Flow
- **Category:** `agents/meeting-assistant-flow`
- **Frameworks & Technologies Used:** Python, Flask, Google ADK, Gemini API, MCP, Google Calendar API, OAuth/OpenID Connect, SQLite, OS keychain.

### Description

A meeting-planning web app with a single-request workflow that automatically prepares a description/agenda and searches shared slots from a meeting name, date, and invitees. It saves editable drafts, calculates candidate slots from permitted free/busy data through a local MCP tool, and prepares agendas using one ADK agent. An exact invitation preview and explicit user approval are required before Calendar creation. Existing meetings' agendas and titles are not fetched. Stable event IDs, version checks, conflict rechecks, and operation reconciliation protect against duplicate and uncertain writes.

## Contribution Checklist

- [x] **Directory & Naming:** Self-contained under `agents/meeting-assistant-flow/`.
- [x] **Documentation:** README follows the repository template and includes setup, architecture, usage, privacy boundaries, and limitations.
- [x] **Reproducible Setup:** Installed `requirements-dev.txt` in a new Python 3.12 virtual environment on macOS; all 103 tests and `pip check` pass there.
- [ ] **Core Functionality Tested:** Automated workflow tests pass, and live sign-in/free-busy access is verified. Live Gemini output, new write-scope consent, and a user-approved real test invitation still need verification before submission.
- [x] **Example Usage:** README includes a real automated synthetic workflow, explicitly distinguished from live provider results.
- [x] **Dependencies Declared:** Runtime and test dependencies are declared in separate manifests.
- [x] **Secrets & Security:** Local `.env`, client JSON, SQLite records, and credentials are excluded by Git. No actual local credential values were found in candidate contribution files. `.env.example` contains placeholders only.
- [x] **Scope Limitation:** Proposed contribution is limited to this directory. Stage only this project; unrelated pre-existing untracked files and the earlier ErrorQuest starter are not part of this PR.

## Testing & Verification Notes

- Python 3.12.13 on macOS, with a fresh isolated environment under `/tmp`.
- `python -m pytest -q`: **103 passed**.
- `python -m pip check`: no broken requirements.
- Real MCP stdio subprocess and actual ADK runner with a synthetic offline model.
- Synthetic Calendar provider for creation tests; no automated test sends real invitations.
- Browser smoke check using a separate disposable account/database: save a draft, calculate slots, show unknown-availability warning, and render the final preview with two explicit approval checks.
- Security tests cover OAuth claim/signature checks, account isolation, partial grants, secret blocking, CSRF, current-version approval, conflict rechecks, duplicate submissions, status-recovery races, and uncertain-write reconciliation.
- Live Google account sign-in and read-only free/busy access were verified separately. A Gemini API key and additional Calendar event consent remain user setup steps.

No commit, push, or pull request has been created yet. Complete the unchecked live verification before submitting.

- Automatic planning tests cover request validation, secret/privacy blocking, HTML escaping, repeated requests, model data minimization, visible template fallback, automatic slot refresh after edits, unknown calendars, and approval-gated creation.

- Natural conversation handles missing date/email, exact-time checks, slot searches, and scheduling; the ADK runner is tested issuing a real function call into the read-only scheduling boundary. Browser refresh clears chats via a CSRF-protected reset. Specific calendar access errors are shown without raw provider responses.
