---
name: rembg
description: Quita el fondo de imágenes localmente con rembg (CLI ya instalado, modelos U2-Net/ISNet vía ONNX). Úsala cuando el usuario pida quitar/eliminar el fondo de una foto, recorte de sujeto, fondo transparente, PNG sin fondo, o preparar imágenes de producto/retrato para diseño. Todo local, sin nube.
---

# rembg — quitar fondos localmente

CLI oficial de rembg, ya instalado vía pip. Procesa en la máquina; ninguna imagen sale a internet.

## Uso

```bash
rembg i "entrada.jpg" "salida.png"
```

- La salida es PNG con transparencia.
- Carpeta completa: `rembg p "carpeta_in" "carpeta_out"`
- Modelo alternativo para retratos finos (pelo): `rembg i -m isnet-general-use in.jpg out.png`
- Máscara en vez de recorte: añade `-om`; matting alfa para bordes suaves: `-a`.

## Notas

- **Primera ejecución**: descarga el modelo (~170 MB, U2-Net) desde los releases oficiales de GitHub a `~/.u2net/`. Avisa al usuario la primera vez.
- Para lotes grandes, procesa con `rembg p` (una sola carga de modelo) en lugar de invocar `rembg i` por archivo.
- Si el resultado deja halos, prueba `-a` (alpha matting) o el modelo `isnet-general-use`.
- Complementa a las skills de diseño (banner-design, design): primero recorta aquí, luego compón.
