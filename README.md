# Effect CI standalone demo

This repository demonstrates the same package tasks locally and at the pushed Git HEAD on a remote Effect CI host. Use Node 24.11+ or 26+ and a checkout of the Effect CI testbed CLI on PATH.

```sh
cf-ci list
cf-ci run build
cf-ci run build
```

Vite+ owns task caching. Change `src/message.js`, run the build again, and inspect `dist/message.js`.

## Remote

Put your deployed host settings in the ignored `.env.local`:

```dotenv
EFFECT_CI_REMOTE_URL=https://<your-worker-hostname>
EFFECT_CI_REMOTE_TOKEN=<your-host-api-token>
CF_ACCESS_CLIENT_ID=<your-access-client-id>
CF_ACCESS_CLIENT_SECRET=<your-access-client-secret>
```

```sh
cf-ci run build --remote
```

Remote execution checks out this repository’s origin at its pushed HEAD and discovers the root package tasks. Commit and push changes first; dirty worktrees are rejected. No target runs all discovered tasks. The host needs the repository-discovery implementation; older hosts run a fixed recipe. Custom Effect workflow modules are not supported by repository discovery yet.
