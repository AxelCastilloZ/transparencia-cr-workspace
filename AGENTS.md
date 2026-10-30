# Workspace — Guía de navegación raíz

**TL;DR:** Workspace de IA para Transparencia Datos CR. Código en `Repos/src/`,
conocimiento en `Knowledge/`, procedimientos en `Skills/`.

## Estructura

| Directorio    | Qué contiene                                    |
| :------------ | :---------------------------------------------- |
| `Knowledge/`  | Documentación durable: dominio, arquitectura    |
| `Skills/`     | Playbooks reutilizables (como slash commands)    |
| `Repos/`      | Symlink al código (git-ignored)                  |
| `temp/`       | Scratch space (git-ignored)                      |

## Convenciones

- Cada directorio tiene un `AGENTS.md` — leé el TL;DR antes de entrar.
- `Knowledge/` y `Skills/` tienen `INDEX.md` — consultalo antes de buscar.
- Los commits del workspace van a `transparencia-cr-workspace` en GitHub.
- Los commits de código van a `transparencia-datos-cr` en GitHub.
- Para OpenSpec: navegá a `Repos/src/transparencia-datos-cr/` y ejecutá allí.
