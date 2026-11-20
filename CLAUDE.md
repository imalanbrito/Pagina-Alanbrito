# CLAUDE.md: hub de redes de @imalanbrito

## Qué es este proyecto

Un Linktree casero: la página que va en la bio de todas mis redes. Se publica en GitHub Pages como **https://imalanbrito.github.io** (el repo se tiene que llamar exactamente `imalanbrito.github.io`).

El objetivo es **engagement**: que alguien que llega desde un TikTok o un Reel termine siguiéndome en otra red, sobre todo en Twitch cuando estoy en vivo. Además, la página tiene que estar llena de mi personalidad, no parecer una plantilla.

## Quién soy (para escribir el copy con mi voz)

- Alan, `@imalanbrito`. Estudiante de último semestre de Ingeniería de Software (UPAEP, Puebla) y Junior Python Developer.
- Hago streams en Twitch (`imalanbritoo`, con doble "o") y los recorto en clips para TikTok, Reels y Shorts. En YouTube (`@imalanbrito`) subo resúmenes de stream con edición y humor; mi referencia es Alpharad.
- Dev de IA y Python: visión por computadora con YOLO (larvas, cultivos de brócoli). Estoy construyendo **streamcut**, una herramienta open source para editar streams con IA.
- Maker: imprimo en 3D (Ender 3), tengo un openGrid y un pegboard SKÅDIS en la pared, y ando armando algo con una Raspberry Pi 5.
- Me gusta Zelda (tengo el proyecto r/OcarinaBard).
- Tono: casual, autoburla ligera, mexicano pero entendible. Bilingüe, porque quiero hacer contenido en inglés sobre código, IA y tech.

## Concepto de diseño: "la pared del maker"

La página es un **pegboard**. Cada red es una **etiqueta impresa en 3D** colgada de un gancho: tiene líneas de capa visibles, un orificio arriba y se balancea en su gancho cuando la tocas. Arriba va una **placa** con mi nombre y dos tornillos. Abajo, "En lo que ando" son tiras de **cinta de rotuladora** (estilo P-touch).

Al agregar algo nuevo, piensa qué objeto físico de mi taller sería y hazlo así. No metas tarjetas genéricas.

### Tokens

| Rol | Valor |
|---|---|
| Tablero | `--board #D5D9CF`, agujeros `--hole #9EA497` |
| Tinta | `--ink #1F2427`, secundaria `--ink-soft #4A5257` |
| Placa | `--plate #F4F5F0` |
| Filamento Twitch | `#7446D8` (texto blanco) |
| Filamento YouTube | `#CF3626` (texto blanco) |
| Filamento TikTok | `#22B8B0` (texto tinta) |
| Filamento Instagram | `#F08A24` (texto tinta) |
| Filamento GitHub | `#2A3035` "PLA galaxia" con brillitos |
| Filamento LinkedIn | `#F7F7F2` PLA blanco (texto tinta) |

- Tipografía: **Unbounded** 800 para mi nombre y los títulos de las etiquetas; **Atkinson Hyperlegible** para todo lo demás (Google Fonts).
- La retícula del pegboard es `--grid: 28px`.

### Reglas de diseño (respétalas)

- El protagonista son las etiquetas colgantes. Todo lo demás se queda tranquilo.
- Movimiento: solo la animación de entrada (`hang`, las etiquetas caen a sus ganchos) y el balanceo (`swing`) cuando alguien pasa el cursor o enfoca una etiqueta. No agregues fade-ins por sección ni animaciones decorativas. Siempre respeta `prefers-reduced-motion`.
- Nada de: etiquetas en MAYÚSCULAS sobre cada título, flechas `→` en los links, separadores con punto medio `·`, fondos negros con neón ni degradados de relleno.
- Contraste accesible: si un filamento es claro, el texto va en tinta, no en blanco.
- Foco visible: como las etiquetas usan `mask` (que recorta el outline), el foco se dibuja en el contenedor `.slot:has(.tag:focus-visible)`.
- Mobile first: una columna en celular, dos desde 680px. La mayoría de las visitas llega desde el celular por la bio.

## Estructura del código

Por ahora todo vive en un solo `index.html` (CSS y JS en línea), a propósito: es fácil de previsualizar y no necesita build.

- **`CONFIG`** (al inicio del `<script>`) es lo único que normalmente se edita:
  - `links[]`: `{ id, style, url, enabled, es: {title, sub}, en: {title, sub} }`. `style` elige el filamento (`twitch | youtube | tiktok | instagram | github | linkedin`). Si agregas una red nueva, crea su clase `.t-<style>` en el CSS.
  - `text.es` / `text.en`: la bio, "En lo que ando", el pie de página y el texto de "en vivo".
  - `twitchUser`: lo usa el detector de "en vivo".
- **`render()`** vuelve a pintar todo; se llama al inicio y al cambiar de idioma. La animación `drop` solo corre en el primer render.
- **`checkLive()`** consulta `https://decapi.me/twitch/uptime/<user>` cada 2 minutos. Si la respuesta no dice "offline", activa `.is-live` en la etiqueta de Twitch. Si el servicio falla, no pasa nada.
- **`track(id)`** manda el clic a GoatCounter si el script está instalado (aún no lo está; ver README).
- El idioma se guarda en `localStorage` dentro de un `try/catch`.
- Si la foto (`github.com/imalanbrito.png`) no carga, se reemplaza por un monograma con mi inicial.

Si el archivo crece mucho, es válido separarlo en `styles.css`, `config.js` y `app.js`, pero mantén `CONFIG` fácil de encontrar y editar.

## Pendientes (TODO)

- [ ] Confirmar los usuarios de TikTok e Instagram (en el código están como suposición: `@imalanbrito`).
- [ ] Poner mi URL real de LinkedIn (hoy es `TU-USUARIO`).
- [ ] Decidir el nombre de la placa ("Alan", "Alan Brito", ...).
- [ ] ¿Agregar Discord, X, r/OcarinaBard o LiniumTech?
- [ ] Instalar GoatCounter para medir clics.
- [ ] Ideas de engagement para después: video o clip destacado arriba que se actualice solo, links con UTM por red de origen (`?from=tiktok`) e imagen OG propia para la vista previa al compartir (1200×630).

## Cómo probar

- Abre `index.html` directo en el navegador, o usa `python3 -m http.server` en la carpeta.
- Revisa en 390px (iPhone) y en escritorio. Revisa que se pueda navegar con el teclado y prueba la versión con movimiento reducido.
- Para ver el estado "en vivo" sin estar transmitiendo, corre esto en la consola: `document.querySelectorAll('.t-twitch').forEach(e => e.classList.add('is-live'))`

## Publicar

Haz push a `main` en el repo `imalanbrito.github.io` y activa Settings → Pages → Deploy from branch → `main` / root.
