# CLAUDE.md — reqit-catalog

## What This Is

This is the **reqit catalog** — a self-hosted web application for managing academic catalogs and requirements (Phase 3). It provides a full UI for catalog CRUD, a visual requirement builder, REST API, and MCP server for AI integration.

## Project Family

Reqit is organized as 4 sibling projects:

| Project | What | Visibility |
|---------|------|-----------|
| **reqit-specs** | Design docs, case studies, strategy, materials | Private |
| **reqit-sdk** | Phase 1 — `reqit` npm package: parser, AST, resolver, auditor, exporters | Open source |
| **reqit-pg** | Phase 2 — `reqit-pg` npm package: PostgreSQL schema, materialization, rollover | Open source |
| **reqit-catalog** (this repo) | Phase 3 — Self-hosted web app: Express 5, Pug, HTMX, Bootstrap 5, PostgreSQL | Open source |

**Dependency chain:** reqit-sdk → reqit-pg → reqit-catalog

All design documents live in `../reqit-specs/design/`. Read `../reqit-specs/design/strategy.md` for the master plan.

## Key Specs

These design documents define what this application implements:

| Spec | What |
|------|------|
| [07-ui-builder.md](../reqit-specs/design/07-ui-builder.md) | Visual requirement builder UI |
| [11-mcp-server.md](../reqit-specs/design/11-mcp-server.md) | MCP server for AI integration |
| [14-user-management.md](../reqit-specs/design/14-user-management.md) | Auth, roles, permissions |
| [15-rest-api.md](../reqit-specs/design/15-rest-api.md) | REST API specification |
| [16-mcp-oauth.md](../reqit-specs/design/16-mcp-oauth.md) | OAuth 2.0 for MCP, BYOLLM |
| [18-ui-components.md](../reqit-specs/design/18-ui-components.md) | HTMX components, CSS isolation |
| [21-branding.md](../reqit-specs/design/21-branding.md) | Fonts, colors, Bootstrap theme, white-label |

## Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Templates:** Pug
- **Interactivity:** HTMX
- **CSS:** Bootstrap 5
- **Database:** PostgreSQL
- **Icons:** Font Awesome (not Bootstrap Icons)

## What This Application Does

- **Catalog management** — CRUD for courses, programs, degrees, attainments, academic years
- **Requirement editing** — Text editor (reqit DSL) and visual drag-and-drop builder
- **Requirement visualization** — Render requirements as trees, outlines, descriptions
- **Export** — XLSX, CSV, JSON, HTML catalog exports
- **REST API** — Full catalog API for external integrations
- **MCP server** — Model Context Protocol endpoint for AI-assisted advising, auditing, planning
- **User management** — Authentication, roles (admin, editor, viewer), permissions
- **White-label** — Configurable branding (fonts, colors, logo)

## Dependencies

- **reqit-sdk** — Parser, AST, resolver, auditor, exporters
- **reqit-pg** — Database schema, materialization, queries

## Critical Constraints

- **No SPA frameworks.** No React, Vue, Angular. Server-rendered with HTMX for interactivity.
- **Font Awesome for all icons.** No Bootstrap Icons.
- **FERPA boundary:** Reqit never stores student data. Transcripts are in-memory input to `audit()`.
- **Single-tenant.** This application serves one institution per deployment.

## What NOT to Do

- Do not use React, Vue, Angular, or any SPA framework
- Do not use Bootstrap Icons — use Font Awesome
- Do not store student data
- Do not implement multi-tenancy — this is a single-tenant application
- Do not implement billing/payment — this is open source software
- Do not duplicate parser/AST/schema logic — depend on reqit-sdk and reqit-pg
