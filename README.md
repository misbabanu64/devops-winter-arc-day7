# DevOps Winter Arc - Day 7: Git, GitHub & Reverse Proxy Troubleshooting

## Project Overview
This project demonstrates professional Git branching and merging workflows alongside configuring Nginx as a reverse proxy for a local backend service.

## Verification & Testing
- Git repository tracked locally and pushed to GitHub with multiple feature branches.
- Tested branch merging and executed a GitHub Pull Request workflow for `feature/health-check`.
- Python HTTP backend running on port 3000.
- Nginx reverse proxy configured to route `http://day7.local` to `http://127.0.0.1:3000`.

## Git Workflow Followed
1. Initialized repository with proper identity and commit structure.
2. Created feature branches (`feature/status-page`, `feature/health-check`).
3. Merged changes locally and through GitHub Pull Requests.
4. Added `.gitignore` to prevent tracking runtime logs and dependencies.

## Production Incident Breakdown
- **Issue**: Simulated a 502 Bad Gateway by terminating upstream service.
- **Investigation**: Inspected `/var/log/nginx/error.log` identifying `111: Connection refused`.
- **Resolution**: Restored upstream process and verified 200 OK status recovery. Full report documented in `incident-report.md`.
