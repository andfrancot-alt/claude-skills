---
name: skyreels-api
description: Genera video con SkyReels V3 (Skywork) vía APIs hospedadas, sin GPU local — reference-to-video (1-4 imágenes de referencia → video con identidad consistente de personaje/producto), extensión de videos existentes con continuidad de movimiento, y avatares parlantes. Úsala cuando el usuario mencione SkyReels, pida extender/alargar un video existente, generar video a partir de imágenes de referencia manteniendo la identidad, o compare SkyReels con otros modelos de video. Requiere WAVESPEED_API_KEY en el entorno (PiAPI como alternativa para image-to-video V1).
---

# SkyReels vía API

SkyReels V3 es el modelo de video open-source de Skywork (arquitectura autoregresiva de difusión). Correrlo localmente exige GPUs de datacenter, así que esta skill usa sus APIs hospedadas. Proveedor principal: **WaveSpeedAI** (endpoints V3 completos, polling documentado). Alternativa: **PiAPI** (solo V1 image-to-video, más barato).

## Claves — siempre desde el entorno

Lee la clave con `$env:WAVESPEED_API_KEY` (o `$WAVESPEED_API_KEY` en bash). Nunca la escribas en archivos, comandos de ejemplo para el usuario, ni la muestres en salida. Si no está configurada, detente y dile al usuario dónde obtenerla (wavespeed.ai → dashboard → API keys) y cómo exportarla; no continúes con placeholders.

## Costos — confirmar antes de gastar

Cada llamada cuesta dinero real. Antes de enviar cualquier request de pago, di el costo estimado y espera confirmación del usuario, salvo que ya la haya dado para ese lote.

| Operación | Precio |
|---|---|
| reference-to-video / extend-video | $0.04 por segundo ($0.20 los 5s, $0.40 los 10s) |
| PiAPI img2video (V1) | $0.15 por generación |

## Endpoints WaveSpeed (V3)

Autenticación en todos: header `Authorization: Bearer $WAVESPEED_API_KEY`, `Content-Type: application/json`.

**Reference-to-video** — 1-4 imágenes anclan identidad/estilo; el prompt controla acción y cámara:

```
POST https://api.wavespeed.ai/api/v3/skywork-ai/skyreels-v3/reference-to-video
{ "prompt": "...", "images": ["https://..."], "aspect_ratio": "16:9|9:16|1:1", "duration": 5 }
```

`images` requiere URLs públicas (no rutas locales). Si el usuario tiene archivos locales, súbelos primero a un hosting que controle (por ejemplo un bucket propio) o pídele una URL; no los subas a servicios de terceros sin avisarle. `duration`: 5-10 segundos.

**Extend-video** — continúa un video existente con coherencia:

```
POST https://api.wavespeed.ai/api/v3/skywork-ai/skyreels-v3/extend-video
{ "prompt": "qué pasa a continuación", "video": "https://...mp4", "duration": 5 }
```

Variantes disponibles con el mismo patrón: `skyreels-v3/extend-video-cutshot` (extensión con corte de plano) y `skyreels-v3-pro/multi-avatar` (avatares parlantes; ver nota ética abajo).

## Obtener el resultado (polling)

La respuesta del POST trae un `request_id` (en `data.id`). Luego:

```
GET https://api.wavespeed.ai/api/v3/predictions/{request_id}/result
```

Repite hasta que `status` sea `completed` (o `failed` — reporta el error tal cual). La generación tarda decenas de segundos: sondea cada ~10s, no en bucle cerrado. El video queda en `data.outputs[0]`; descárgalo con `curl -o <destino>.mp4 <url>` y entrega la ruta local, no solo la URL (las URLs de resultado pueden expirar).

## Alternativa PiAPI (V1, image-to-video simple)

Si el usuario solo quiere animar una imagen y tiene `PIAPI_KEY`:

```
POST https://api.piapi.ai/api/v1/task    (header: x-api-key)
{ "model": "Qubico/skyreels", "task_type": "img2video",
  "input": { "prompt": "...", "image": "url o base64", "aspect_ratio": "16:9", "guidance_scale": 3.5 } }
```

Nota: V1 es un modelo anterior y de menor calidad que V3; úsalo solo por costo o si no hay clave de WaveSpeed.

## Nota ética

Para `multi-avatar` o cualquier generación que anime el rostro de una persona real, confirma que el usuario tiene consentimiento de esa persona antes de enviar la petición. Misma política que la skill faceswap.

## Cuándo NO usar esta skill

Para generación de video general sin requisito de SkyReels (texto→video genérico), la skill `ai-video-gen` enruta entre más proveedores (VEO, Kling, Sora, Seedance…) y suele ser mejor punto de partida. Esta skill es para cuando SkyReels aporta lo suyo: identidad consistente desde referencias, extensión de video, o petición explícita del usuario.
