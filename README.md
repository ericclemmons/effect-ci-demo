# Effect CI pnpm demo

This branch runs the existing Vite+ project with pnpm and no authored CI workflow.
Use Node 24.11+ or 26+ and the Effect CI testbed CLI on PATH.

```sh
pnpm install --frozen-lockfile
effect-ci list
effect-ci run build --local
effect-ci run build
effect-ci run build --remote
```

The public `.cloudflare/ci/oidc.json` selects the existing hosted service.
Ordinary runs dispatch the clean, pushed HEAD remotely. Authenticate as an operator
through the host’s Cloudflare Access policy. `--local` runs working-tree edits.
Remote failures do not run tasks locally.

Vite+ owns task fingerprints and cache hits. The host transports
`node_modules/.vite/task-cache` between runs; a restored snapshot alone does not
prove a task hit. Change `src/message.js`, commit and push, then run build again
to check invalidation. This branch does not deploy the demo or add a GitHub workflow.
