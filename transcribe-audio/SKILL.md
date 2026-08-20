---
name: transcribe-audio
description: Transcribe audio localmente con faster-whisper (ya instalado, 4x más rápido que Whisper clásico en CPU). Úsala cuando el usuario pida transcribir un audio, nota de voz, grabación, entrevista, dictado o podcast (MP3, WAV, M4A, OGG, opus) a texto, con o sin timestamps. Todo local, sin nube. Para VIDEOS usa la skill video-understand (extrae frames + transcribe); esta es para archivos de audio puro.
---

# transcribe-audio — faster-whisper local

Transcripción local con faster-whisper (CTranslate2). Nada sube a la nube.

## Uso (vía python inline)

```bash
python -c "
from faster_whisper import WhisperModel
model = WhisperModel('base', compute_type='int8')
segments, info = model.transcribe(r'RUTA_AUDIO', language='es')
for s in segments: print(f'[{s.start:.1f}s] {s.text.strip()}')
"
```

- `language='es'` para español (detecta solo si se omite, pero fijarlo es más rápido y fiable).
- Modelos: `base` (rápido, default), `small` (mejor), `medium`/`large-v3` (máxima calidad, más lentos). El modelo se descarga de HuggingFace la primera vez (~150 MB el base); avisa al usuario.
- Para texto corrido sin timestamps, concatena `s.text` y entrega en un archivo `.md` o `.txt` si el audio es largo.
- Audio con varios hablantes: faster-whisper no diariza; adviértelo si piden "quién dijo qué".

## Cuándo NO usarla

- Video → `video-understand` (pipeline completo frames+audio).
- Doblaje/traducción de video → `video-translate`.
