# Transparencia Datos CR — Overview

## Qué es

Sistema web monorepo que integra cuatro fuentes de datos públicos de Costa Rica,
indexados por cantón, en un "Radar Cantonal de Señales Públicas".

## Repositorio

- **GitHub:** `git@github.com:AxelCastilloZ/transparencia-datos-cr.git`
- **Ruta local:** ver `Repos/repos.local.json`

## Arquitectura

```
┌─────────────┐     ┌──────────────────┐     ┌──────────────┐
│   Frontend   │────▶│     Backend      │────▶│  PostgreSQL  │
│  React+Vite  │     │     NestJS       │     │  (Supabase)  │
│  Tailwind v4 │     │    TypeORM       │     │              │
└─────────────┘     └──────────────────┘     └──────────────┘
                          │
               ┌──────────┼──────────┐──────────┐
               ▼          ▼          ▼          ▼
            OIJ/CSV    SICOP/API   TSE/ZIP   DatosAbiertos
```

## Módulos de fuentes

| Módulo        | Fuente                          | Responsable | Estado     |
| :------------ | :------------------------------ | :---------- | :--------- |
| OIJ (Judicial)| CSVs estadísticas policiales    | Axel        | Completado |
| SICOP         | API órdenes de compra           | Compañero A | Completado |
| TSE           | Padrón electoral (PADRON.TXT)   | Compañero B | Completado |
| Datos Abiertos| datosabiertos.presidencia.go.cr | Compañero C | Completado |
| Radar         | Integración de las 4 fuentes    | Equipo      | Completado |

## Endpoints principales

| Método | Ruta                            | Descripción                    |
| :----- | :------------------------------ | :----------------------------- |
| GET    | `/api/cantones`                 | Lista 84 cantones              |
| GET    | `/api/radar/canton/:codigo`     | Ficha integrada del cantón     |
| GET    | `/api/judicial/canton/:codigo`  | Estadísticas policiales        |
| GET    | `/api/judicial/resumen`         | Top delitos                    |
| GET    | `/api/judicial/mensual`         | Incidentes por mes             |
| GET    | `/api/health`                   | Health check                   |
| POST   | `/api/judicial/sync`            | Sincronizar datos OIJ          |

## DevSecOps

Pipeline SSDLC con 12 ítems implementados:
- CI: lint + test + build + Gitleaks + Semgrep + OSV-Scanner + Trivy
- Dockerfiles multi-stage + SBOM (CycloneDX)
- Pre-commit hooks (Gitleaks)
- E2E tests (Playwright)
- Health check + Docker HEALTHCHECK
- Deploy workflow a GHCR

Ver `openspec/specs/devsecops-ssdlc.md` en el repo del proyecto para detalles.

## Restricciones críticas

1. **TSE:** NUNCA persistir datos personales (cédula, nombre)
2. **SICOP:** DEBE separar montos por moneda (CRC/USD)
3. **TypeORM:** `synchronize: true` — no crear migraciones manuales
4. **Package manager:** Solo pnpm, nunca npm/yarn
