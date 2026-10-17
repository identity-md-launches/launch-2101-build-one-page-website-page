# hello world

A one-page website whose entire visible content is `hello world`, with no authored styling or client JavaScript. The finished static export is included in `dist/`.

## Install, preview, and rebuild

Use Node.js 22.12 or newer and npm. Install the exact locked development dependencies:

```sh
npm ci
npm run typecheck
npm run build
npm run preview
```

Open the local address printed by Vite. Stop the preview with Ctrl+C. `npm run dev` starts the development server when editing. The production preview serves `dist/`, so rebuild after source changes. You can also open `dist/index.html` directly; the exported page does not need a server-side application.

The build uses [Vite's relative base](https://vite.dev/guide/build.html#relative-base), configured as `./` in `vite.config.ts`. Upload the **contents of `dist/` together** to any static host or gateway subpath. There is only one page and no routing or backend. The favicon and share image are local. `og:image` is relative because the eventual hosting URL is not known; a social platform's actual unfurl remains unverified until hosting.

## Files

- `index.html`: complete page source and metadata.
- `public/`: SVG favicon and PNG share image, copied to the export.
- `vite.config.ts`, `tsconfig.json`: build configuration and strict typecheck settings.
- `package.json`, `package-lock.json`: pinned development toolchain; no runtime dependencies.
- `dist/`: production HTML and both runtime assets; include this in the submission.
- `DESIGN.md`: implemented browser-default design and six-domain review context.
- `artifacts/`: validation report, measured results, screenshots, and guidance license notices.

Do not add generated dependencies, caches, or package archives to a submission. No ignore file was created or changed. The worker installed dependencies only in disposable `test/scratch/` copies and kept npm/browser caches outside the delivered files.

## Validation performed

The worker ran the following against the final source/export:

| Check | Actual result |
| --- | --- |
| Clean dependency install | `npm ci --prefix test/scratch/build-check --no-audit --no-fund --cache /tmp/hello-world-npm-cache`: exit 0. The scratch directory contained an exact copy of source and lockfile. |
| Typecheck | `npm run typecheck --prefix test/scratch/build-check`: exit 0. Checks `vite.config.ts`; there is no client TypeScript. |
| Production build | `npm run build --prefix test/scratch/build-check`: exit 0. Its complete `dist/` was copied to the repository root. |
| Pinned taste probe | `node .imd/reads/skills/design-critic/scripts/taste.mjs --out test/scratch/taste`, with `IMD_PLAYWRIGHT` pointing to the scratch installation and `PLAYWRIGHT_BROWSERS_PATH` to the temporary browser directory: exit 0, **16/16 checks passed**. |
| Browser validation | `PLAYWRIGHT_BROWSERS_PATH=/tmp/hello-world-browsers node test/scratch/validate.mjs`: final run exit 0. Chromium passed loading, reload, direct subpath access, native keyboard selection, JavaScript-disabled rendering, metadata/assets, and responsive checks. |
| Accessibility automation | axe WCAG A/AA tag scan in Chromium: 0 violations, 0 incomplete results, 6 applicable checks passed. This is not full accessibility certification. |

The initial browser harness hit a thread/resource limit while running alongside the inspection browser. It passed after the inspection browser was closed and contexts were run sequentially. The final scan ran axe directly in the existing page. WebKit launch remained unavailable because system libraries were missing; no WebKit pass is claimed.

The worker inspected actual mobile and desktop screenshots. Chromium checks covered 320, 390, 768, and 1440px widths; all showed the complete greeting without horizontal overflow. Native zoom, physical devices, and screen-reader sessions were not tested. Detailed six-domain coverage, findings, and evidence are in [artifacts/validation.md](artifacts/validation.md). Scratch scripts and pinned inputs are temporary and are not part of the delivered app; their measured results are retained in `artifacts/`.
