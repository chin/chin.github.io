# Architecture decisions

Entries are proposals for review. A status of **Proposed** means the scaffold demonstrates the choice but the owner has not approved it for the next implementation phase.

## ADR-001 — Deployment platform

- **Date:** 2026-10-01
- **Status:** Proposed
- **Context:** The brief requires GitHub Pages, static hosting, and no unnecessary backend or hosted service.
- **Decision:** Generate static files and deploy them to GitHub Pages using GitHub Actions artifacts. Do not configure a custom domain or canonical origin without confirmation.
- **Alternatives:** Direct branch publishing; another static host; server-based hosting.
- **Rationale:** Astro requires a build; GitHub's Pages custom-workflow guidance supports generated artifacts and least-privilege deployment permissions. Actions keeps the build reproducible from the repository and allows pull-request validation.
- **Consequences:** GitHub Pages repository settings must select Actions; workflow needs `pages: write` and `id-token: write` only for deploy. PR validation gets no deploy permissions. External Pages configuration remains unverified.
- **Reversibility:** High. Generated static output can be hosted elsewhere; workflow and host configuration change.
- **Evidence:** [GitHub Pages custom workflows](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages), [GitHub deployment permissions](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).

## ADR-002 — Framework and build model

- **Date:** 2026-10-01
- **Status:** Proposed
- **Context:** The site needs multiple information areas, reusable layouts, static output, light client behavior, and likely structured projects/research/writing later.
- **Decision:** Use Astro in static/prerendered mode. Keep the current scaffold minimal and defer content collection schemas until actual authored entries exist.
- **Alternatives:**
  - Plain HTML/CSS/JS: smallest build and dependency footprint, but repeated page shells and growing structured content would need manual conventions or new tooling.
  - Eleventy: credible low-runtime SSG with many template languages, layouts, collections, data files, and a local server; less built-in typed content validation, and its flexibility means choosing and maintaining template conventions.
  - Astro: a build dependency and Node toolchain, but provides component/layout composition, file routes, and typed/schema-validated collections while outputting static HTML by default.
- **Rationale:** Astro's composition and optional schema validation match anticipated structured content. Static generation preserves fast, crawlable HTML and no client runtime is needed for this type of site. This is a capability-based choice, not a fashion choice.
- **Consequences:** Node/npm and lockfile become part of reproduction and updates. Framework templates/config are less portable than raw HTML, though `dist/` is ordinary static output. Keep integrations and browser JS absent unless a need is demonstrated.
- **Reversibility:** Medium. Content and generated output are portable; source templates/config/scripts require migration.
- **Evidence:** [Astro pages and file routes](https://docs.astro.build/en/basics/astro-pages/), [Astro content collections and schemas](https://docs.astro.build/en/guides/content-collections/), [Astro static GitHub Pages deployment](https://docs.astro.build/en/guides/deploy/github/), [Astro install and Node requirements](https://docs.astro.build/en/install-and-setup/), [Eleventy official getting started](https://www.11ty.dev/docs/).

## ADR-003 — Design-system strategy

- **Date:** 2026-10-01
- **Status:** Proposed
- **Context:** The site needs a distinct technical identity, not a generic branded product UI. Mature systems provide useful patterns, but their visual assets/components may add dependency and customization costs.
- **Decision:** Use a small original CSS token layer and semantic HTML. Treat Primer, USWDS, IBM Carbon, Shoelace/Web Awesome, and ESnet's Packets system as references, not installed dependencies or sources of copied branding.
- **Alternatives and research:**
  - Primer: MIT licensed and actively maintained in its wider organization, but Primer CSS itself reports KTLO status and is recognizably GitHub's system; not adopted.
  - USWDS: strong accessibility documentation and modular packages; its conventions and components serve federal service needs and carry visual/utility scope unnecessary here.
  - Carbon: mature, Apache-2.0 implementation with accessibility guidance, but broad framework/component package and IBM-specific visual identity exceed this site's need.
  - Shoelace: mature web-component approach, but the original repository/site now points toward Web Awesome; adding a UI runtime is unjustified for the present static content site.
  - ESnet Packets: relevant research-network design system; useful as a technical organization reference, but not a necessary dependency for a personal site.
- **Rationale:** A small token layer makes identity ownership explicit, avoids framework coupling, visual imitation, unused components, and ongoing dependency upgrades. Research informs accessible patterns; it is not a license to copy another organization's look.
- **Consequences:** We own token choices, semantic markup, and manual accessibility review. External component-level accessibility benefits are not inherited.
- **Reversibility:** High while tokens and CSS remain small; adding a design system later would affect CSS architecture and markup.
- **Evidence:** [Primer CSS license and KTLO status](https://github.com/primer/css), [USWDS accessibility guidance](https://designsystem.digital.gov/documentation/accessibility/), [USWDS packages](https://designsystem.digital.gov/components/packages/), [Carbon accessibility guide](https://github.com/carbon-design-system/carbon/blob/main/docs/guides/accessibility.md), [Shoelace repository status](https://github.com/shoelace-style/shoelace), [ESnet Packets design system](https://github.com/esnet/packets-design-system).

## ADR-004 — Styling strategy

- **Date:** 2026-10-01
- **Status:** Proposed
- **Context:** The visual direction is restrained, legible, responsive, and original; current scaffold does not need a utility framework, Sass, or visual effects.
- **Decision:** Use plain CSS and a compact custom-property token layer once a visual direction is reviewed. Use system font stacks by default, semantic document flow, and progressive responsive layout.
- **Alternatives:** Adopt Primer/USWDS/Carbon CSS; utility CSS framework; preprocessor; external font service.
- **Rationale:** Platform CSS supports the current need without additional packages, runtime code, external font requests, or organizational branding. Tokens can capture the limited recurring values and remain owner-readable.
- **Consequences:** Project owns token naming and responsive/accessibility verification. Avoid premature tokenization and do not implement the final visual system in this phase.
- **Reversibility:** High if CSS remains scoped and tokens small.
- **Evidence:** [USWDS token model](https://designsystem.digital.gov/design-tokens/), [Primer CSS organization and license](https://github.com/primer/css).

## ADR-005 — Content architecture

- **Date:** 2026-10-01
- **Status:** Proposed
- **Context:** Expected subject areas include home, identity/about, research, projects/portfolio, writing/publications, and contact/external links. Content is not yet supplied.
- **Decision:** Use a small multi-page structure. Keep route/navigation metadata separate from page presentation. When real repeated project, research, or writing records are ready, model them as local structured content and add schemas; do not establish a CMS or empty content model now.
- **Alternatives:** One long page; independent hand-written standalone pages; CMS-backed site.
- **Rationale:** Distinct subject areas merit direct URLs and metadata, while a home page can connect them. Local authored content keeps Git the source of truth. Astro collections can validate repeated records when there is real data.
- **Consequences:** Route labels and navigation hierarchy need owner/content review. Adding collections later establishes a schema contract. No content claims are made in the scaffold.
- **Reversibility:** Medium. Routes and content organization can be changed before launch; after indexing, redirects and canonical links may be needed.
- **Evidence:** [Astro file-based routes](https://docs.astro.build/en/basics/astro-pages/), [Astro collection schemas and guidance on when not to create a collection](https://docs.astro.build/en/guides/content-collections/).

## ADR-006 — CI/CD strategy

- **Date:** 2026-10-01
- **Status:** Proposed
- **Context:** Static generation requires a reproducible build before deployment. Pull requests should receive validation without deploy authority.
- **Decision:** Use a GitHub Actions workflow: PRs build only; pushes to `main` build, package only `dist/`, and deploy via Pages. Pin actions to reviewed immutable commit SHAs (with release tags in comments), minimize permissions, and do not use secrets. Configure Pages source to GitHub Actions separately in repository settings.
- **Alternatives:** Direct branch publishing; deploy every PR; manually build/upload output.
- **Rationale:** CI catches build failures before merge and the Pages artifact/deployment model publishes the exact built static output. PR workflow has read-only repository access and cannot deploy, including PRs from forks.
- **Consequences:** Workflow assumes `main`, GitHub Actions enabled, and Pages configured. SHA pins must be deliberately updated when action fixes/security releases are adopted. Astro/Node upgrades also require deliberate review. Repository UI settings are not managed by this repo.
- **Reversibility:** High; workflow can be replaced without changing page/content source.
- **Evidence:** [GitHub Pages custom workflows](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages), [Astro GitHub Pages guide](https://docs.astro.build/en/guides/deploy/github/), [GitHub Actions permissions](https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication).
