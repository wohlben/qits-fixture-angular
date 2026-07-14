# qits-fixture-angular

A minimal but **servable** Angular SPA used as a qits test/demo fixture. It is the frontend
half of the [`qits-fixture-quarkus-angular`](https://github.com/wohlben/qits-fixture-quarkus-angular)
fixture, extracted into its own repository so it can be exercised **two ways**:

- **Standalone Angular-only workspace** — framework detection resolves to Angular, the SPA serves
  with no backend, the qits **capture button** self-hides via its `OPTIONS` availability probe
  (there is no ingest to talk to), and `withQitsSnapshot` state capture and `@qits/angular`
  consumption are all exercised without a Quarkus server.
- **`src/main/webui` submodule** of `qits-fixture-quarkus-angular` — recomposed back into the
  full-stack fixture via a *relative-url* submodule (`../qits-fixture-angular.git`), which resolves
  to GitHub for humans and to the qits git host inside a workspace container.

## Branches

| Branch | Relationship | Content |
|---|---|---|
| `main` | base | the full instrumented SPA |
| `feature/greeting` | **fast-forward** over `main` | adds a welcome note under the greeting (`src/app/greeting.ts`) |
| `feature/diverged` | **conflicts** with `main` | rewords the greeting off an earlier base — a real text conflict in `greeting.ts` |

## Dependencies

The SPA consumes [`@qits/angular`](https://github.com/wohlben/qits-angular) — the qits instrumentation
library — as a SHA-pinned git dependency (`git+https://github.com/wohlben/qits-angular.git#<sha>`).
`pnpm install` fetches it from GitHub exactly as in the composed fixture.

## Build & run

```bash
pnpm install
pnpm build           # ng build → dist/
pnpm start           # ng serve; API proxies to :8080 if a backend is up, else the capture button self-hides
```

Requires JDK-free tooling: Node + pnpm only (see `packageManager` in `package.json`).
