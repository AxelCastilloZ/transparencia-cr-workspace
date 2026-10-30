# Transparencia CR — Workspace

Workspace de IA para el proyecto [Transparencia Datos CR](https://github.com/AxelCastilloZ/transparencia-datos-cr). No contiene código fuente — el código vive en su propio repo y se accede desde aquí vía symlink.

## Requisitos previos

- Git
- [Node.js 22+](https://nodejs.org/)
- [pnpm](https://pnpm.io/) (`corepack enable && corepack prepare pnpm@latest --activate`)
- [Claude Code](https://claude.ai/code) u otro agente de IA compatible

## Setup rápido

### 1. Cloná ambos repos en la misma carpeta

```bash
cd ~/proyectos   # o la carpeta que prefieras
git clone git@github.com:AxelCastilloZ/transparencia-datos-cr.git
git clone git@github.com:AxelCastilloZ/transparencia-cr-workspace.git
```

Tu estructura queda así:

```
~/proyectos/
├── transparencia-datos-cr/         ← Código del proyecto
└── transparencia-cr-workspace/     ← Este workspace
```

### 2. Creá el symlink al código

Desde dentro del workspace, enlazá la carpeta padre donde están tus repos:

```bash
cd transparencia-cr-workspace
ln -s ~/proyectos ./Repos/src
```

Verificá que funcione:

```bash
ls Repos/src/transparencia-datos-cr/
# Deberías ver: backend/  frontend/  package.json  ...
```

### 3. Creá tu config local

```bash
cat > Repos/repos.local.json << 'EOF'
{
  "reposRoot": "/home/TU_USUARIO/proyectos",
  "junction": "Repos/src",
  "resolvedExample": "Repos/src/transparencia-datos-cr"
}
EOF
```

Reemplazá `/home/TU_USUARIO/proyectos` con tu ruta real.

### 4. Instalá dependencias del proyecto

```bash
cd Repos/src/transparencia-datos-cr
pnpm install
```

### 5. Configurá el backend

Pedile a Axel la variable `DATABASE_URL` y creá el archivo `.env`:

```bash
cat > backend/.env << 'EOF'
DATABASE_URL=postgresql://...tu-url-aqui...
EOF
```

### 6. Verificá que todo funcione

```bash
pnpm test    # 82 tests deben pasar (69 backend + 13 frontend)
pnpm build   # Debe compilar sin errores
```

## Cómo trabajar

1. **Abrí Claude Code desde el workspace**, no desde el repo de código:

```bash
cd ~/proyectos/transparencia-cr-workspace
claude
```

2. El agente lee `CLAUDE.md` y sabe navegar: código en `Repos/src/`, documentación en `Knowledge/`, procedimientos en `Skills/`.

3. **Los commits de código** van al repo del proyecto (`transparencia-datos-cr`).

4. **Los commits del workspace** (Knowledge, Skills) van a este repo.

## Cómo contribuir al proyecto DevSecOps

1. Cambiá a la rama `development` del proyecto:

```bash
cd Repos/src/transparencia-datos-cr
git checkout development
git pull
```

2. Creá tu rama personal:

```bash
git checkout -b feature/TU_NOMBRE-devsecops
```

3. Revisá tus tareas asignadas:

```bash
cat openspec/changes/devsecops-pendientes/tasks.md
```

4. Completá tus ítems, commiteá y abrí un PR a `development`.

## Estructura del workspace

```
transparencia-cr-workspace/
├── CLAUDE.md              # Instrucciones para el agente de IA
├── AGENTS.md              # Navegación raíz (progressive disclosure)
├── Knowledge/             # Documentación durable
│   ├── INDEX.md           # Tabla de contenidos
│   └── Systems/
│       └── TransparenciaCR/overview.md
├── Skills/                # Playbooks reutilizables
│   ├── INDEX.md
│   └── devsecops-review/SKILL.md
├── Repos/                 # Código enlazado (git-ignored)
│   ├── AGENTS.md
│   ├── .gitkeep
│   ├── repos.local.json   # Config local (git-ignored)
│   └── src -> ~/proyectos # Symlink (git-ignored)
└── temp/                  # Scratch space (git-ignored)
```

## Qué se commitea y qué no

| Se commitea (workspace)           | NO se commitea                    |
| :-------------------------------- | :-------------------------------- |
| CLAUDE.md, AGENTS.md              | Repos/src (symlink)               |
| Knowledge/ (docs)                 | repos.local.json (rutas locales)  |
| Skills/ (playbooks)               | temp/ (scratch)                   |
| .gitignore                        | El código del proyecto             |
