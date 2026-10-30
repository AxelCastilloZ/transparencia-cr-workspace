# Transparencia CR — Workspace

Este es el workspace de IA para el proyecto Transparencia Datos CR.
No contiene código fuente — el código vive en un repo separado accesible
vía symlink en `Repos/src/`.

## Navegación

1. Leé primero `AGENTS.md` (esta carpeta) para orientarte.
2. Si necesitás contexto de negocio o arquitectura → `Knowledge/`.
3. Si necesitás un procedimiento estandarizado → `Skills/`.
4. Si necesitás tocar código → `Repos/src/transparencia-datos-cr/`.

## Reglas generales

- **Nunca commitear código al workspace.** El código va al repo del proyecto.
- **Nunca commitear secretos.** El `.env` del backend es git-ignored.
- Este workspace se commitea: Knowledge, Skills, CLAUDE.md, AGENTS.md.
- El código se commitea al repo del proyecto en GitHub.

## Stack del proyecto

- **Backend:** NestJS + TypeORM + PostgreSQL (Supabase)
- **Frontend:** React + Vite + TypeScript + Tailwind CSS v4 + Recharts
- **Monorepo:** pnpm workspaces (`backend/`, `frontend/`)
- **CI/CD:** GitHub Actions (lint, test, SAST, SCA, Trivy)

## Repos enlazados

Leé `Repos/repos.local.json` para la ruta local. El proyecto está en:
`Repos/src/transparencia-datos-cr/`

## OpenSpec

Las specs y changes de OpenSpec viven dentro del repo del proyecto
(`<repo>/openspec/`), no aquí. Desde este workspace, navegá al repo
y ejecutá comandos de OpenSpec allí:

```bash
cd Repos/src/transparencia-datos-cr
openspec list
openspec status --change devsecops-pendientes
```

## Restricciones críticas del proyecto

- El módulo TSE **NUNCA** debe persistir datos personales (cédula, nombre).
- SICOP **DEBE** separar montos por moneda (CRC/USD), nunca sumar mixto.
- TypeORM usa `synchronize: true` — NO crear migraciones manuales.
- Instalar siempre con `pnpm install` desde la raíz del proyecto, nunca npm/yarn.
- Fecha límite proyecto DevSecOps: **13 de noviembre de 2026**.
