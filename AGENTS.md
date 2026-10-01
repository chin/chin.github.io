# Repository operating contract

## Before changing the site

- Read `ARCHITECTURE.md`, `STATUS.md`, `DECISIONS.md`, and `TASKS.md` before substantial work.
- Inspect the existing implementation and Git status before editing. Preserve existing behavior unless a change is intentional.
- Prefer simple, explicit solutions. Do not add dependencies, duplicate responsibilities, rewrite working code, or change architecture for stylistic preference without a documented reason.
- Do not invent biography, accomplishments, metrics, affiliations, publications, credentials, project descriptions, research results, or citations. Mark missing facts `[CONTENT NEEDED]` and unresolved choices explicitly.

## Human control

For a substantial architectural change not already authorized by the owner:

1. Explain the proposed change, affected files, and tradeoffs.
2. Wait for approval before implementing it.

Do not silently cross architectural boundaries or continue beyond the review checkpoint in `STATUS.md`.

## Dependencies

Before adding a dependency, explain why it is needed, whether platform capabilities suffice, runtime/build impact, maintenance and upgrade burden, license, and whether a smaller implementation is preferable. Document material decisions in `DECISIONS.md`.

## Content and security

- Keep presentation, content, navigation, metadata, and visual tokens in distinct responsibilities; do not duplicate the same content across components.
- Never commit API keys, tokens, passwords, private certificates, SSH keys, personal access tokens, or secrets in environment files.
- Inspect `.gitignore` and CI configuration when changing dependencies or workflows.
- Do not add a backend, database, authentication, CMS, analytics, or third-party service without a demonstrated requirement and owner approval.

## Accessibility and performance

- Use semantic HTML, logical headings, keyboard-operable controls, visible focus, appropriate image alternatives, and a skip link when navigation is present.
- Check contrast, responsive text sizing, screen-reader behavior, and reduced-motion behavior (`prefers-reduced-motion`) as visual work is added.
- Do not rely on color or animation alone to convey meaning. Navigation must not depend on animation.
- Avoid unnecessary JavaScript, third-party scripts, web fonts, image payloads, animation, hydration, and runtime dependencies. Prefer static output.
- Give each major visual treatment a reason tied to hierarchy, navigation, technical communication, identity, or interaction. Do not add decorative effects merely because they are available.

## Validation and reporting

- After changes, run applicable project checks and a production build; inspect build output and use a production preview when practical.
- Report exact commands and results. Never claim a check that was not run.
- Keep changes relevant to the task. Do not rewrite Git history, force-push, delete branches, or alter repository settings without explicit authorization.
