# Pagina alanbrito

Mi hub de redes: un pegboard con etiquetas impresas en 3D colgadas de ganchos.

## Publicarlo

1. En GitHub, crea un repo **público** llamado exactamente `imalanbrito.github.io`.
2. Sube `index.html` (y este README) a la rama `main`.
3. En el repo ve a **Settings → Pages**, en *Source* elige **Deploy from a branch**, rama `main`, carpeta `/ (root)`.
4. En uno o dos minutos queda en **https://imalanbrito.github.io**. Esa es la URL para tus bios.

## Editarlo

Todo vive en el objeto `CONFIG` al inicio del `<script>` en `index.html`:

- `links`: cada etiqueta. Cambia `url`, los textos `es`/`en`, o usa `enabled: false` para esconderla.
- `text`: la bio, la sección "En lo que ando" y el pie de página, en ambos idiomas.
- `avatar`: hoy usa tu foto de GitHub. Para usar otra, sube `avatar.jpg` y pon `avatar: "avatar.jpg"`.

## Detector de "en vivo"

La etiqueta de Twitch revisa cada 2 minutos con DecAPI si `imalanbritoo` está transmitiendo. Si lo estás, aparece "En vivo ahora". Si el servicio falla, la etiqueta se queda normal.

## Medir clics (opcional, gratis)

1. Crea una cuenta en goatcounter.com (por ejemplo con el código `imalanbrito`).
2. Pega esto antes de `</body>`:

```html
<script data-goatcounter="https://imalanbrito.goatcounter.com/count"
        async src="//gc.zgo.at/count.js"></script>
```

Cada clic en una etiqueta se registra como `click/twitch`, `click/youtube`, etc.
