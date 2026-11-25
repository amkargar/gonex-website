<p align="center">
  <a href="https://amkargar.github.io/gonex-website/">
    <img src="public/brand/duck.webp" alt="Gonex duck mascot" width="148">
  </a>
</p>

<h1 align="center">Gonex Website</h1>

<p align="center">
  The home of Gonex — guides, examples and project notes.<br>
  Built with Nuxt. Published as a fully static website.
</p>

<p align="center">
  <a href="https://amkargar.github.io/gonex-website/"><strong>Visit website</strong></a> ·
  <a href="https://amkargar.github.io/gonex-website/docs/main/">Documentation</a> ·
  <a href="https://amkargar.github.io/gonex-website/docs/main/quick-start/">Get started</a> ·
  <a href="https://github.com/amkargar/gonex">Framework source</a>
</p>

<p align="center">
  <a href="https://github.com/amkargar/gonex-website/actions/workflows/deploy.yml"><img src="https://github.com/amkargar/gonex-website/actions/workflows/deploy.yml/badge.svg" alt="Website deployment"></a>
  <img src="https://img.shields.io/badge/Nuxt-4-00DC82?logo=nuxt&logoColor=white" alt="Nuxt 4">
  <img src="https://img.shields.io/badge/Node.js-24-5FA04E?logo=nodedotjs&logoColor=white" alt="Node.js 24">
</p>

## A small home for a growing framework

This repository contains the website for [Gonex](https://github.com/amkargar/gonex), an API-first Go framework. It helps developers build applications, explore the framework and contribute to its development.

- **Build with Gonex:** installation, CLI, JSON APIs, logging and deployment.
- **Contribute to Gonex:** architecture, internals, testing and maintenance.
- **Find your way:** versioned guides, local full-text search and keyboard navigation.
- **Read comfortably:** responsive layouts, light/dark themes and copyable code examples.
- **Follow the project:** Markdown journal, categories and RSS.

Nuxt 4 · TypeScript · Tailwind CSS 4 · Nuxt UI · Nuxt Content. Fonts and search are local; production hosting serves static files.

## Run locally

Use **Node.js 24 LTS** and npm. The build uses native `node:sqlite`.

```sh
npm ci
npm run dev
```

Preview indexing is disabled by default. See [.env.example](.env.example) for configuration.

| Command | Purpose |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run typecheck` | Check TypeScript |
| `npm run verify:docs` | Check documentation consistency |
| `npm run generate` | Export and audit the static website |
| `npm run preview` | Preview the generated output |
| `npm run sync-content` | Refresh navigation and search indexes |

`npm run build` also generates the static export. Output is **`.output/public`**; no application server is needed in production.

## Write and update content

| Location | Contents |
| --- | --- |
| `content/docs/main/` | Development documentation |
| `content/blog/` | Journal articles |
| `shared/versions.json` | Documentation versions and default version |
| `shared/source-snapshot.json` | Reviewed upstream source commit |
| `examples/api/` | Standalone consumer Go example |
| `public/` | Mascot, fonts, icons and social image |

Docs use `title`, `description`, `order`, `version`, `section` (`build` or `contribute`) and `group` in frontmatter. Adapted guides can include a `source` reference. Blog posts also use `date`, `author`, `category` and `readingTime`.

Use readable filenames and root-relative links such as `/docs/main/modules/`. NuxtLink adds the deployment base automatically; use `useSiteUrl().asset()` for raw assets. When adding a page during development, run `npm run sync-content` and restart the dev server.

<details>
<summary><strong>Versions and upstream updates</strong></summary>

To add a documentation version, create `content/docs/<version>/` with an `index.md` and its guides, then register it in `shared/versions.json`. Assign each page its section, group and order. Set the release state accurately and change `defaultVersion` only when appropriate. Run typecheck and generation before publishing.

The selector preserves the current guide when it exists in the destination version. Documentation versions and application HTTP API versions are independent.

Import upstream changes deliberately, preserving website frontmatter and local links. Update `shared/source-snapshot.json` and keep source references pinned to the reviewed commit. Check actual release/toolchain status before updating installation instructions.

`main · Development` represents a source snapshot, not a tagged framework release. Documentation does not synchronize automatically, and building the website does not execute its Go examples.

</details>

## Publish to GitHub Pages

In **Settings → Pages → Build and deployment**, select **GitHub Actions**. Push to `main` or run [Deploy Gonex Website](https://github.com/amkargar/gonex-website/actions/workflows/deploy.yml) manually.

The workflow installs dependencies, checks types, generates and audits the output, then publishes `.output/public`. GitHub supplies the origin and base path, including custom-domain settings.

For a manual production export:

```sh
SITE_URL=https://amkargar.github.io NUXT_APP_BASE_URL=/gonex-website/ PUBLIC_INDEXING=true npm run generate
```

PowerShell:

```powershell
$env:SITE_URL = "https://amkargar.github.io"
$env:NUXT_APP_BASE_URL = "/gonex-website/"
$env:PUBLIC_INDEXING = "true"
npm run generate
```

Keep `SITE_URL` as an HTTPS origin without a path. Configure the path separately through `NUXT_APP_BASE_URL`; use `/` for root deployments. Leave `PUBLIC_INDEXING=false` for private previews.

## Quality and discoverability

Pages export full HTML with canonical URLs, social metadata and structured data. Generation also prepares sitemap, robots rules, RSS, icons, webmanifest and optional `llms.txt`.

The static checker validates exported routes, headings, metadata, local links/assets and indexing policy. See [VERIFICATION.md](VERIFICATION.md) for recorded checks and their limits. Browser accessibility, search indexing and rankings require separate verification; `llms.txt` is not a ranking signal.

## Credits and licensing

Imported framework documentation follows the upstream **BSD 3-Clause** license: [UPSTREAM_LICENSE](UPSTREAM_LICENSE). First-party website files and articles were delivered to the project owner without a separate license grant here. Local fonts include their license files in `public/fonts/`; the mascot was supplied by the owner.

Journal drafts describe the project and its architecture; they are not release announcements or endorsements.
