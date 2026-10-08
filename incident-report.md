# Production Incident Report - INC-001

## Incident Summary
- **Service Affected**: day7.local (Reverse Proxy & Backend)
- **Status Code Returned**: HTTP 502 Bad Gateway
- **Duration**: ~5 minutes
- **Impact**: Backend application unavailable to end users

## Root Cause Analysis
- The backend application listening on port 3000 was terminated (process stopped).
- Nginx reverse proxy received incoming client requests on port 80 but could not establish a TCP handshake with upstream `127.0.0.1:3000`.
- Log evidence from `/var/log/nginx/error.log`:
  `connect() failed (111: Connection refused) while connecting to upstream`

## Resolution & Recovery
- Restarted backend Python HTTP server process on port 3000.
- Verified service availability via Nginx reverse proxy using curl:
  - `curl -I http://day7.local` -> HTTP/1.1 200 OK
  - Verified body content: "Day 7 Production App HEALTHY"

## Prevention Measures
- Configure a process manager (such as `systemd` or `supervisor`) to automatically restart the backend application on failure.
- Implement proactive health-check monitoring and alert mechanisms.
