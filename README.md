# Dr. Chin — Quantum Systems & Platform Architect

This repository is the source of truth for the website. The current page is an unfinished, noindex scaffold for validating the static build architecture.

Read `STATUS.md` for the current checkpoint, `ARCHITECTURE.md` for how the site is organized, and `DECISIONS.md` for proposed choices and evidence.

## Local development

Use Node 24 and npm:

```sh
npm ci
export ASTRO_TELEMETRY_DISABLED=1
npm run dev
npm run build
npm run preview
```

Astro's CLI otherwise attempts to store its telemetry preference in the user's home directory. The Pages workflow disables Astro telemetry explicitly.

See `TASKS.md` for the next reviewable work. Do not add factual content without owner-provided information.
