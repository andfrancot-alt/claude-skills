# claude-skills

Skills personales de Claude Code, versionadas para respaldo y sincronización entre máquinas.

Esta carpeta vive en `~/.claude/skills/` — Claude Code carga automáticamente cada subcarpeta que contenga un `SKILL.md`.

## Skills

| Skill | Descripción |
|-------|-------------|
| [graphify](graphify/SKILL.md) | Convierte cualquier input (código, docs, papers, imágenes, videos) en un grafo de conocimiento persistente, con consultas vía `graphify query`. |

## Uso en otra máquina

```sh
git clone git@github.com:andfrancot-alt/claude-skills.git ~/.claude/skills
```

(Si `~/.claude/skills` ya existe con contenido, clonar a un lado y fusionar manualmente.)

## Convenciones

- Una skill = una carpeta con `SKILL.md` (frontmatter `name` + `description`) y opcionalmente `references/`, `scripts/`, `assets/`.
- Las salidas generadas por las skills (p. ej. `graphify-out/`) no se versionan aquí; viven en cada proyecto.
- Skills específicas de un proyecto van en el `.claude/skills/` de ese proyecto, no en este repo.
