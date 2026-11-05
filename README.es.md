# seo-audit-specialist

[English](README.md)

Skill de agente para **SEO full-stack** en Claude Code, Cursor y Codex. No se queda en una lista de consejos. Ejecuta el bucle del consultor:

**diagnostica render/indexación → prioriza hallazgos por impacto SEO → entrega arreglos exactos de código y contenido → avisa de los errores que matan posiciones**

> **Repositorio:** [JuanAn-WD/seo-audit-specialist](https://github.com/JuanAn-WD/seo-audit-specialist).

## Instalación (un comando)

```bash
npx skills add JuanAn-WD/seo-audit-specialist -a claude-code -a cursor -a codex
```

Usa el CLI open-source [`skills`](https://github.com/vercel-labs/skills). Copia la carpeta de la skill en `.agents/skills/` (Cursor y Codex) y la enlaza en `.claude/skills/` (Claude Code). Añade `-g` para instalarla a nivel de usuario en vez del proyecto actual.

Métodos de instalación alternativos: [más abajo](#otros-métodos-de-instalación).

## Qué incluye

| Skill | Úsala cuando | Qué hace |
| --- | --- | --- |
| `seo-audit-specialist` | "Mejora el SEO de esta web", "¿Es indexable esta página de Next/Nuxt?", "Arregla nuestros Core Web Vitals" | Actúa como consultor senior de SEO técnico para aplicaciones web modernas (**Vue / Nuxt / React / Next.js**). Audita renderizado e indexabilidad (CSR vs SSR/SSG), el head dinámico (`<title>`, canonical, Open Graph), Core Web Vitals (LCP, CLS, INP), HTML semántico, enlazado rastreable, Schema.org JSON-LD y estrategia de keywords/intención — y entrega el informe priorizado con las soluciones listas para copiar y pegar. |

## Cómo audita

Especializada en Vue (Vue Router, Unhead, Nuxt) y React (React Router, Helmet/Async, Next.js). Tres pilares, siempre en orden:

1. **SEO técnico y arquitectura** — ¿el contenido crítico depende solo de JavaScript en el cliente? ¿El head se gestiona con `useSeoMeta`/`unhead` (Nuxt) o con la Metadata API/`react-helmet-async` (Next)? ¿Toda la navegación es un `<a>` real en el DOM?
2. **SEO on-page y HTML semántico** — un único `<h1>` por vista con la keyword principal; `<main>`/`<header>`/`<nav>` en vez de divitis; `alt` descriptivos y nombres de archivo semánticos; JSON-LD válido (Article, Product, FAQPage, BreadcrumbList, Organization, WebSite).
3. **Estrategia y contenido** — alineación con la intención de búsqueda; arquitectura de keywords principales, secundarias y semánticas (LSI); títulos de 50–60 caracteres y meta descripciones de 120–155 escritas para CTR.

## Cómo reporta

- Cada hallazgo se clasifica **[IMPACTO CRÍTICO]** (bloqueos de indexación, falta de SSR en contenido vital, navegación no rastreable con `onClick`, LCP/CLS graves), **[IMPACTO MEDIO]** (falta de JSON-LD, jerarquía de encabezados rota, HTML no semántico, imágenes sin `alt` o dimensiones) o **[IMPACTO BAJO]** (copy para CTR, Open Graph secundario, micro-optimizaciones de URLs), siempre con el **Problema** y su **Impacto en SEO**.
- Justo después del diagnóstico viene el **plan implementable**: el componente refactorizado (HTML semántico, API de metadatos, `fetchpriority`, dimensiones, JSON-LD) si la entrada fue código, o el `<title>`, meta descripción y estructura H1–H3 exactos si la entrada fue contenido.
- Errores típicos sobre los que avisa siempre: la obsoleta `<meta name="keywords">`, metadatos inyectados solo en el cliente para bots sociales que no ejecutan JavaScript (WhatsApp, X, LinkedIn, Facebook) y trucos de cloaking que penalizan accesibilidad y ranking.

## Comparación

| | Prompt genérico "mejora mi SEO" | Herramientas formales de auditoría (Screaming Frog, Lighthouse) | **seo-audit-specialist** |
| --- | --- | --- | --- |
| Objetivo | Consejos rápidos | Checklist de rastreo del sitio vivo | Arreglos específicos del framework con código |
| Conoce las APIs de head de Vue/Nuxt/React | No | Parcialmente | Sí: `useHead`/`useSeoMeta`, Unhead, Metadata API de Next |
| Informe priorizado por impacto | No | Datos de rastreo, sin encuadre de negocio | Sí: crítico / medio / bajo con problema + impacto |
| Entrega el arreglo | Rara vez | No (solo informes) | Sí: componente refactorizado o contenido listo |
| Generación de JSON-LD | Rara vez | Solo validadores | Genera bloques válidos listos para inyectar |
| Detecta trampas de indexación en SPAs | Suele ignorarlas | Las señala, no las arregla | Avisa de metadatos CSR-only para crawlers sociales |

Siendo justos: las herramientas de rastreo ven el sitio vivo y escalan a millones de URLs. Úsalas también si tu sitio es grande — esta skill es la capa experta que convierte hallazgos en arreglos concretos en el código de tu framework. Las dos formas funcionan bien juntas.

## Otros métodos de instalación

Copia la carpeta única `skills/seo-audit-specialist` (el `SKILL.md` en la raíz del repo es el mismo archivo).

### Claude Code

```bash
git clone https://github.com/JuanAn-WD/seo-audit-specialist /tmp/seo-audit-specialist
mkdir -p .claude/skills && cp -R /tmp/seo-audit-specialist/skills/. .claude/skills/
```

O copia manualmente la carpeta en `.claude/skills/` (proyecto) o `~/.claude/skills/` (usuario).

### Codex

Copia la carpeta en `.agents/skills/` (repo) o `~/.agents/skills/` (usuario).

### Cursor

Copia la carpeta en `.cursor/skills/` o `.agents/skills/` (proyecto), o `~/.cursor/skills/` (usuario). Cursor también lee skills de `.claude/skills/` y `.codex/skills/`.

**Aviso:** esta skill es una ayuda de ingeniería, no una garantía de posiciones. El resultado SEO depende de la competencia, el historial del dominio y la calidad del contenido más allá de cualquier auditoría.
