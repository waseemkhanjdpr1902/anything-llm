# Deploy SayItLLM on Railway

Source: `waseemkhanjdpr1902/anything-llm`, branch `master`, repository root. The tracked `railway.json` selects `docker/Dockerfile` and the `/api/ping` healthcheck. Build from this repository to include SayItLLM branding; the upstream prebuilt image does not contain these changes.

## Hosting prerequisites

An active Railway plan is required: project creation was blocked because the connected account's trial expired. No SayItLLM project or service was created by that attempt.

## Deployment configuration

- Create a service connected to this GitHub repository and `master` branch.
- Attach a persistent volume at `/app/server/storage` before first use.
- Set `STORAGE_DIR=/app/server/storage`, `SERVER_PORT=3001`, `NODE_ENV=production`, `DISABLE_TELEMETRY=true`.
- Generate and securely configure independent random `JWT_SECRET`, `SIG_KEY`, and `SIG_SALT` values (at least 32 characters). Do not commit secrets. Keep signing values stable across redeployments.
- Ensure the volume is writable by the image's application user (UID/GID 1000 by default). Diagnose mount permissions from runtime logs if startup fails.
- Keep one replica for this SQLite/local-storage configuration.
- Wait for a healthy deployment, then route a Railway domain to container port 3001. Protect the initial setup from untrusted access; complete authentication setup before sharing the URL.

## First run and verification

Complete onboarding, enable multi-user mode and create the admin account as appropriate. Configure your model provider and embedding provider with their required credentials. Provider usage may incur separate charges.

Verify login, a normal chat, upload and embed a small document, then ask a question grounded in that document. Redeploy and confirm the account, workspace and document data survive. Confirm the UI shows SayItLLM. Configure backups before customer use.

This deployment does not add subscription billing or usage-based customer plans. Browser testing and a full source build remain pending until hosting is available.
