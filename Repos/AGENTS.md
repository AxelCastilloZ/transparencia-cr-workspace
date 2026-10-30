# Repos — Código enlazado

**TL;DR:** Aquí se enlazan los repos de código vía symlink. Todo está git-ignored
excepto este archivo y `.gitkeep`.

## Cómo funciona

- `src/` es un symlink a la carpeta donde vivien los repos de código.
- `repos.local.json` tiene la ruta local (git-ignored, cada máquina la configura).
- Para acceder al proyecto: `Repos/src/transparencia-datos-cr/`.

## Setup en tu máquina

```bash
ln -s /ruta/a/tus/repos ./Repos/src
```

Luego creá `Repos/repos.local.json`:

```json
{
  "reposRoot": "/ruta/a/tus/repos",
  "junction": "Repos/src",
  "resolvedExample": "Repos/src/transparencia-datos-cr"
}
```
