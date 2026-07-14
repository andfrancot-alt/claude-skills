# claude-skills

Skills personales de Claude Code, versionadas para respaldo y sincronización entre máquinas.

Esta carpeta vive en `~/.claude/skills/` — Claude Code carga automáticamente cada subcarpeta que contenga un `SKILL.md`.

## Skills

### Propias

| Skill | Descripción |
|-------|-------------|
| [graphify](graphify/SKILL.md) | Convierte cualquier input (código, docs, papers, imágenes, videos) en un grafo de conocimiento persistente, con consultas vía `graphify query`. |
| [grill-me](grill-me/SKILL.md) | Entrevista implacable sobre un plan o diseño hasta lograr entendimiento compartido, recorriendo el árbol de decisiones. |

### Video — generación y edición (origen: [OpenMontage](https://github.com/calesthio/OpenMontage), MIT; auditadas 2026-07-14)

**Locales, sin claves API:**

| Skill | Descripción |
|-------|-------------|
| [video-edit](video-edit/SKILL.md) | Edición local con ffmpeg: cortar, unir, redimensionar, velocidad, overlay, comprimir, convertir. |
| [ffmpeg](ffmpeg/SKILL.md) | Procesamiento de video/audio con FFmpeg y preparación de assets para Remotion. |
| [video-download](video-download/SKILL.md) | Descarga de video/audio/subtítulos con yt-dlp (YouTube y 1000+ sitios). |
| [video-understand](video-understand/SKILL.md) | Análisis local de contenido: frames con ffmpeg + transcripción Whisper. |
| [remotion-best-practices](remotion-best-practices/SKILL.md) | Buenas prácticas de Remotion (video programático en React). |

**Con API de nube (requieren clave HeyGen / fal.ai / etc.):**

| Skill | Descripción |
|-------|-------------|
| [create-video](create-video/SKILL.md) | Prompt→video con HeyGen Video Agent. |
| [avatar-video](avatar-video/SKILL.md) | Videos de avatar con control fino (avatares, voces, escenas) vía HeyGen v2. |
| [video-translate](video-translate/SKILL.md) | Traducción y doblaje de videos con lip-sync (HeyGen). |
| [faceswap](faceswap/SKILL.md) | Face swap en video vía HeyGen (usar solo con consentimiento de las personas). |
| [ai-video-gen](ai-video-gen/SKILL.md) | Enrutador de generación de video entre proveedores (VEO, Kling, Sora, Runway, Seedance, MiniMax…). |
| [seedance-2-0](seedance-2-0/SKILL.md) | Clips cinematográficos con ByteDance Seedance 2.0 (audio nativo, multi-shot). |
| [ltx2](ltx2/SKILL.md) | Text-to-video / image-to-video con LTX-2.3 22B. |

Excluidas de OpenMontage en la auditoría: `media-use` (instalador `curl \| bash`), `heygen` (deprecada), y las acopladas al framework HyperFrames (`music-to-video`, `website-to-video`, `motion-graphics`, `kling-official`, `video-toolkit`, `remotion`), que no funcionan fuera del repo original.

## Uso en otra máquina

```sh
git clone git@github.com:andfrancot-alt/claude-skills.git ~/.claude/skills
```

(Si `~/.claude/skills` ya existe con contenido, clonar a un lado y fusionar manualmente.)

## Convenciones

- Una skill = una carpeta con `SKILL.md` (frontmatter `name` + `description`) y opcionalmente `references/`, `scripts/`, `assets/`.
- Las salidas generadas por las skills (p. ej. `graphify-out/`) no se versionan aquí; viven en cada proyecto.
- Skills específicas de un proyecto van en el `.claude/skills/` de ese proyecto, no en este repo.
