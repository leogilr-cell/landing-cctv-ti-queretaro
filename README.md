# Landin page — CCTV / Informática / Telecomunicaciones (Querétaro)

Landing page estática, responsiva y de fácil mantenimiento para un negocio de
instalación de CCTV, soporte TI, telecomunicaciones y mejora de señal WiFi en
Santiago de Querétaro, México.

## Stack

- **Astro** (modo estático, `output: 'static'`)
- **Tailwind CSS** (mobile-first)
- **Alpine.js** vía CDN (interactividad: carrusel, contador, FAQ, formulario)
- **Netlify Forms** (captura de leads, sin backend propio)

## Correr el proyecto local

```bash
npm install
npm run dev
```

Abre `http://localhost:4321`.

Para generar el sitio de producción:

```bash
npm run build
```

## Estructura de carpetas

```
/src
  /content
    faq.json            <- preguntas y respuestas (editable, ver abajo)
    site-config.json    <- contactos, textos, servicios, contador (editable)
  /images
    /cctv               <- imágenes de instalaciones de CCTV
    /computacion        <- imágenes de trabajos de informática/TI
    /telecom            <- imágenes de telecomunicaciones
  /components           <- componentes .astro de cada sección
  /layouts
  /pages/index.astro
netlify.toml
```

## Agregar imágenes nuevas al showcase

Simplemente copia tus fotos a las carpetas del directorio correspondiente:

- `src/images/cctv/` para cámaras de seguridad
- `src/images/computacion/` para trabajos de informática/TI
- `src/images/telecom/` para telecomunicaciones y redes

Se aceptan `.jpg`, `.jpeg`, `.png`, `.webp` y `.avif`.

En el siguiente `npm run build` (o push a Netlify) **se incluyen automáticamente
en el carrusel**, sin tocar código. No debes editar nada de diseño:

- No importa repetir una imagen en dos categorías: cada archivo se muestra solo
  una vez.
- Si una carpeta está vacía, la sección muestra un aviso hasta que agregues fotos
  (y sigue funcionando el resto del sitio).

## Editar el FAQ

Abre `src/content/faq.json` y agrega, edita o quita objetos con este formato:

```json
{
  "categoria": "CCTV",
  "pregunta": "Tu pregunta aquí",
  "respuesta": "Tu respuesta aquí"
}
```

Guarda y reconstruye. La búsqueda y el acordeón se actualizan solos.

## Editar textos, contactos y contador

Todo el contenido editable vive en `src/content/site-config.json`:

- `business`: nombre, teléfono, WhatsApp, email, dirección, horarios.
- `seo`: título y descripción meta (CCTV Querétaro, soporte TI Querétaro, etc.).
- `hero`: título y subtítulo del encabezado.
- `services`: las 4 tarjetas de servicios.
- `counter`: `value` es el número de clientes atendidos (lo animas manualmente).
- `links`: URL de reseña en Google y redes sociales.
- `form.categories`: opciones del campo de categoría.
- `mapEmbed`: iframe del mapa.

Nunca edites los componentes `.astro` para cambiar texto: cambia los JSON.

### Número de WhatsApp

En `site-config.json` → `business.whatsapp`, pon solo el número con código de país,
**sin** el `+` ni espacios. Ej: `524421234567`. Los enlaces de WhatsApp del hero,
del botón flotante y del footer salen de ahí automáticamente.

### Contador de clientes

`business` no: es `counter.value`. Es un valor estático que editas a mano
(no se cuenta en tiempo real porque no hay backend). La animación ascendente ya está
implementada y se dispara al hacer scroll.

## Deploy en Netlify

1. Sube el repositorio a Git (GitHub/GitLab/Bitbucket).
2. En Netlify: "Add new site" → "Import an existing project" → conecta tu repo.
3. Netlify lee `netlify.toml` y ejecuta `npm run build`, publicando la carpeta `dist`.
4. En los ajustes del sitio (Site settings → Forms):
   - **Form notifications** → add notification → **Email notification** y escribe el
     correo donde quieres recibir cada lead.
5. Cada vez que hagas `git push` a la rama principal, Netlify reconstruye y publica.

## Exportar leads a CSV (Netlify)

Para clasificar qué categorías de falla son las más recurrentes:

1. En el panel de Netlify entra a **Forms** (del sitio).
2. Selecciona el formulario **"contacto"**.
3. Botón **"Download submissions"** (o **CSV download**) → descarga el archivo CSV.
4. Ábrelo en una hoja de cálculo y filtra por la columna **Categoria del problema**
   para comparar frecuencias.

Los envíos también se notifican por correo (ver arriba).

## Aviso importante antes de publicar

En `src/content/site-config.json` hay placeholders marcados como `[COMPLETAR: ...]`
(nombre del negocio, teléfono, WhatsApp, email, redes). Cámbialos por datos reales
antes del deploy.
