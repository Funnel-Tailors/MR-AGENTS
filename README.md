# MR-AGENTS

Colección de agentes especializados para Claude Code.

## Instalación

```bash
# Clona en la carpeta de agentes de Claude Code
cd ~/.claude
git clone git@github.com:Funnel-Tailors/MR-AGENTS.git agents

# O si ya tienes agentes, inicializa git en tu carpeta existente:
cd ~/.claude/agents
git init
git remote add origin git@github.com:Funnel-Tailors/MR-AGENTS.git
git fetch origin
git merge origin/main --allow-unrelated-histories
```

## Agentes Disponibles (43)

### SEO Workforce (opus)
Pipeline de SEO clásico + GEO/AI search. Cada agente entiende primero el contexto del proyecto y deja documentación persistente en `docs/seo/` del proyecto objetivo. Pueden invocar otros agentes del repo para subir la calidad.

| Agente | Modo | Descripción |
|--------|------|-------------|
| `seo-researcher` | default | Contexto del proyecto, keyword research, intención, análisis de SERP, competidores orgánicos y oportunidades GEO |
| `seo-architect` | plan | Documento de estrategia (arquitectura pillar/cluster, justificación con evidencia, protocolo de calidad), content briefs y QA final |
| `seo-writer` | acceptEdits | Redacción de páginas a partir del brief, en el formato real del proyecto, con autoevaluación contra el protocolo |

**Flujo**: `seo-researcher` → `seo-architect` → `seo-writer` (una instancia por brief) → `seo-architect` (QA)

```
docs/seo/
  00-contexto-proyecto.md   ← researcher
  01-research.md            ← researcher
  02-estrategia-seo.md      ← architect (arquitectura + justificación + tests)
  briefs/<slug>.md          ← architect
  qa/<slug>.md              ← writer (autoevaluación) + architect (validación)
```

**Protocolo de calidad por página**: 10 hard gates pass/fail (intención, keyword, canibalización, respuesta directa, fuentes, enlazado, metadata, schema, conversión, voz) + scorecard 0–100 (information gain, cobertura, E-E-A-T, citabilidad GEO, legibilidad, conversión, enlazado). Se publica con todos los gates en PASS y score ≥ 85.

### Críticos (opus + plan)
Decisiones de alto impacto que requieren análisis profundo y aprobación.

| Agente | Descripción |
|--------|-------------|
| `api-architect` | Diseño de APIs REST/GraphQL con auth, rate limiting, docs |
| `cloud-cost-optimizer` | Reducción de costos AWS, right-sizing, auto-scaling |
| `data-engineer` | Pipelines ETL, data warehouses, streaming |
| `database-optimizer` | Optimización de queries, diseño de esquemas, índices |
| `debug-specialist` | Diagnóstico de bugs, análisis de stack traces |
| `llm-integration-specialist` | Integración de LLMs, RAG, embeddings, prompts |
| `monetization-architect` | Sistemas de pago, pricing, suscripciones |
| `security-expert` | Vulnerabilidades, auth, validación, OWASP |
| `software-architect` | Arquitectura de sistemas, refactoring |
| `sre-reliability-engineer` | SLOs, error budgets, incident response |

### Análisis (opus + default)
Análisis profundo sin modificaciones directas.

| Agente | Descripción |
|--------|-------------|
| `competitive-analyst` | Análisis de competencia, posicionamiento |
| `mobile-game-sprite-artist` | Dirección de arte de sprites/animaciones para juegos móviles, sprite sheets, atlas, specs |
| `premium-motion-auditor` | Auditoría de motion design, animaciones premium estilo Linear/Vercel |
| `product-strategist` | Decisiones build/kill, roadmap, priorización |
| `senior-code-reviewer` | Code review exhaustivo, bugs, seguridad |

### Implementación (sonnet + plan)
Implementación técnica que requiere aprobación.

| Agente | Descripción |
|--------|-------------|
| `automation-architect` | Cron jobs, workflows, pipelines automatizados |
| `design-systems-architect` | Sistemas de diseño, componentes reutilizables |
| `integration-specialist` | Integraciones con servicios externos, webhooks |
| `load-test-engineer` | Tests de carga, stress testing, benchmarks |
| `nextjs-architect` | Arquitectura Next.js, App Router, RSC |
| `observability-specialist` | Monitoring, logging, alerting, dashboards |
| `perf-optimizer` | Optimización de performance, caching |

### Implementación Activa (sonnet + acceptEdits)
Implementan código directamente.

| Agente | Descripción |
|--------|-------------|
| `analytics-implementation-expert` | Tracking de eventos, funnels, métricas |
| `playwright-e2e-expert` | Tests E2E con Playwright |
| `premium-ui-designer` | UI premium, animaciones, micro-interacciones |
| `test-architect` | Tests unitarios, integración, cobertura |
| `ux-pain-point-fixer` | Identificación y fix de problemas UX |
| `ux-simplifier` | Simplificación de interfaces y flujos |

### Análisis Ligero (sonnet + default)
Análisis e investigación sin modificaciones.

| Agente | Descripción |
|--------|-------------|
| `code-improvement-scanner` | Mejoras de código, best practices |
| `design-review-agent` | Review de diseño UI con Playwright |
| `innovation-explorer` | Exploración de tecnologías emergentes |
| `prompt-engineer` | Diseño y optimización de prompts |
| `unique-design-system-architect` | Componentes UI únicos, anti-vibecoding |

### Orquestación (sonnet + delegate)
Coordinan otros agentes.

| Agente | Descripción |
|--------|-------------|
| `orchestration-specialist` | Coordinación multi-dominio |
| `workflow-orchestrator` | Descomposición de tareas complejas |

### Contenido (haiku + default)
Generación de contenido simple.

| Agente | Descripción |
|--------|-------------|
| `email-campaign-architect` | Campañas de email, secuencias, copy |

## Configuración de Agentes

Cada agente tiene un frontmatter YAML con:

```yaml
---
name: nombre-del-agente
description: "Cuándo usar este agente..."
model: opus | sonnet | haiku
mode: plan | acceptEdits | default | delegate
tools: Bash, Glob, Grep, Read, Edit, Write, WebFetch, WebSearch
color: pink | blue | purple | etc
---
```

### Modelos
- **opus**: Decisiones críticas (seguridad, arquitectura, datos, pagos)
- **sonnet**: Implementación técnica sólida
- **haiku**: Generación de contenido simple

### Modos
- **plan**: Requiere aprobación antes de hacer cambios
- **acceptEdits**: Implementa activamente, muestra cambios
- **default**: Solo análisis/lectura
- **delegate**: Puede invocar otros agentes

## Sincronización

```bash
# Obtener cambios del repo
cd ~/.claude/agents
git pull

# Subir cambios
git add -A
git commit -m "descripción del cambio"
git push
```

## Contribuir

1. Crea o modifica un agente
2. Asegúrate de configurar model y mode apropiados
3. Commit y push con descripción clara

---

Mantenido por el equipo de Funnel Tailors
