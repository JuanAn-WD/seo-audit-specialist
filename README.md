# seo-audit-specialist

[Español](README.es.md)

An agent skill for **full-stack SEO** in Claude Code, Cursor and Codex. It doesn't stop at a checklist of ideas. It runs the consultant loop:

**diagnose render/indexing → prioritise findings by SEO impact → deliver exact code + content fixes → flag the gotchas that burn rankings**

> **Repository:** [JuanAn-WD/seo-audit-specialist](https://github.com/JuanAn-WD/seo-audit-specialist).

## Install (one command)

```bash
npx skills add JuanAn-WD/seo-audit-specialist -a claude-code -a cursor -a codex
```

This uses the open-source [`skills` CLI](https://github.com/vercel-labs/skills). It copies the skill folder into `.agents/skills/` (used by Cursor and Codex) and links it into `.claude/skills/` (Claude Code). Add `-g` to install for your user instead of the current project.

Other install methods are [further down](#other-install-methods).

## What's inside

| Skill | Use it when | What it does |
| --- | --- | --- |
| `seo-audit-specialist` | "Improve the SEO of this site", "Is this Next/Nuxt page indexable?", "Fix our Core Web Vitals" | Acts as a senior technical SEO consultant for modern web apps (**Vue / Nuxt / React / Next.js**). Audits rendering and indexability (CSR vs SSR/SSG), the dynamic head (`<title>`, canonical, Open Graph), Core Web Vitals (LCP, CLS, INP), semantic HTML and crawlable linking, Schema.org JSON-LD and keyword/intent strategy — then delivers copy-paste-ready fixes and a prioritised report. |

## How it audits

Specialised for Vue (Vue Router, Unhead, Nuxt) and React (React Router, Helmet/Async, Next.js). Three pillars, always in order:

1. **Technical SEO & architecture** — does critical content depend on client-only JavaScript? Is the head managed via `useSeoMeta`/`unhead` (Nuxt) or the Metadata API/`react-helmet-async` (Next)? Is every navigation a real `<a>` in the DOM?
2. **On-page & semantic HTML** — one `<h1>` per view with the primary keyword; `<main>`/`<header>`/`<nav>` instead of divitis; descriptive `alt` text and file names; valid JSON-LD (Article, Product, FAQPage, BreadcrumbList, Organization, WebSite).
3. **Strategy & content** — search intent alignment; primary/secondary/LSI keyword architecture; 50–60 char titles and 120–155 char meta descriptions written for CTR.

## How it reports

- Every finding is classified **[HIGH IMPACT]** (indexing blockers, missing SSR on vital content, non-crawlable `onClick` navigation, broken LCP/CLS), **[MEDIUM IMPACT]** (missing JSON-LD, broken heading hierarchy, non-semantic HTML, images without `alt` or dimensions) or **[LOW IMPACT]** (CTR copy, secondary Open Graph tags, URL micro-optimisations), each with the **Problem** and its **SEO impact**.
- Right after the diagnosis you get the **implementable plan**: the refactored component (semantic HTML, metadata API, `fetchpriority`, dimensions, JSON-LD) for code input, or the exact `<title>`, meta description and H1–H3 structure for content input.
- Built-in gotchas it will warn you about: obsolete `<meta name="keywords">`, metadata only injected client-side for social bots that never run JavaScript (WhatsApp, X, LinkedIn, Facebook), and cloaking tricks that harm accessibility and rankings.

## Comparison

| | Generic "improve my SEO" prompt | Formal SEO audit tools (Screaming Frog, Lighthouse) | **seo-audit-specialist** |
| --- | --- | --- | --- |
| Main goal | Quick tips | Running-site crawling checklist | Framework-specific fixes with code delivered |
| Knows Vue/Nuxt/React head APIs | No | Partially | Yes: `useHead`/`useSeoMeta`, Unhead, Next Metadata API |
| Prioritised impact report | No | Crawl data, not business framing | Yes: critical / medium / low with problem + impact |
| Delivers the fix | Rarely | No (reports only) | Yes: refactor component or ready-to-paste content |
| JSON-LD generation | Rarely | Validators only | Generates valid blocks ready to inject |
| Catches SPA indexing traps | Often missed | Can flag, doesn't fix | Warns on CSR-only metadata for social crawlers |

To be fair: crawling tools see the live site and scale across millions of URLs. Run them too if your site is large — this skill is the expert layer that turns findings into fixes in your actual framework code. The two approaches work fine together.

## Other install methods

Copy the single folder `skills/seo-audit-specialist` (the `SKILL.md` at the repo root is the same file).

### Claude Code

```bash
git clone https://github.com/JuanAn-WD/seo-audit-specialist /tmp/seo-audit-specialist
mkdir -p .claude/skills && cp -R /tmp/seo-audit-specialist/skills/. .claude/skills/
```

Or manually copy the folder into `.claude/skills/` (project) or `~/.claude/skills/` (user).

### Codex

Copy the folder into `.agents/skills/` (repo) or `~/.agents/skills/` (user).

### Cursor

Copy the folder into `.cursor/skills/` or `.agents/skills/` (project), or `~/.cursor/skills/` (user). Cursor also loads skills from `.claude/skills/` and `.codex/skills/`.

**Disclaimer:** this skill is an engineering aid, not a guarantee of rankings. SEO outcomes depend on competition, domain history and content quality beyond any audit.
