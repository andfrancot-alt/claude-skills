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

### UI/UX — diseño (origen: [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill), auditada 2026-07-14: sin red no documentada, sin inyección, scripts limpios)

| Skill | Descripción |
|-------|-------------|
| [ui-ux-pro-max](ui-ux-pro-max/SKILL.md) | Base de datos local consultable: 84 estilos, 192 paletas, 74 pares tipográficos, guías UX, presets GSAP y charts para 22 stacks. |
| [design](design/SKILL.md) | Generación de logos, iconos, CIP y material social con guías de prompt. |
| [design-system](design-system/SKILL.md) | Tokens de diseño, fondos de slides y lógica de color/layout. |
| [ui-styling](ui-styling/SKILL.md) | Estilado UI con Tailwind/shadcn (incluye `shadcn_add.py`). |
| [brand](brand/SKILL.md) | Guías de marca: identidad visual, voz, tipografía, sincronización a tokens. |
| [slides](slides/SKILL.md) | Presentaciones: layouts, copywriting y plantillas HTML. |
| [banner-design](banner-design/SKILL.md) | Banners: tamaños estándar y estilos. |

### Animación UI (origen: [Emil Kowalski](https://skills.sh/emilkowalski/skills), auditada 2026-07-14: solo markdown, sin código, con defensa anti-inyección propia)

| Skill | Descripción |
|-------|-------------|
| [animation-vocabulary](animation-vocabulary/SKILL.md) | Glosario inverso: describe un efecto de motion vago y devuelve su término exacto. |
| [apple-design](apple-design/SKILL.md) | El enfoque de Apple de diseño y motion físico/fluido, traducido a la web. |
| [emil-design-eng](emil-design-eng/SKILL.md) | Filosofía de Emil Kowalski sobre pulido de UI y detalles invisibles. |
| [improve-animations](improve-animations/SKILL.md) | Auditoría priorizada del motion de un codebase con planes de implementación (read-only). |
| [review-animations](review-animations/SKILL.md) | Review de código de animación con barra alta (solo invocación explícita). |

### Prototipado y diseño HTML (auditada 2026-07-14)

| Skill | Descripción |
|-------|-------------|
| [huashu-design](huashu-design/SKILL.md) | 花叔Design: prototipos HTML de alta fidelidad, slides, animación, visualización y crítica experta. Incluye SFX/BGM, exportación PDF/PPTX/MP4 (requiere `npm install` en su carpeta) y TTS Doubao opcional (clave propia en `.env`, texto va a ByteDance). Skill en chino; opera en cualquier idioma. |

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
