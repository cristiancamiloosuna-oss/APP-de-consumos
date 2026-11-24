# Bolsillo, versión instalable

Esta carpeta es la app completa. No necesita Claude ni servidor propio: solo un sitio gratis donde publicarla. Tus datos se guardan en tu celular, no en internet.

## 1. Publicarla gratis con GitHub Pages (desde el computador)

1. Entra a github.com y crea una cuenta si no tienes.
2. Toca **+ → New repository**. Nombre: `bolsillo`. Déjalo en **Public** y toca **Create repository**.
3. Toca **uploading an existing file** y arrastra todo lo que hay en esta carpeta: `index.html`, `manifest.webmanifest`, `sw.js`, `LEEME.md` y la carpeta `icons`. Luego toca **Commit changes**.
4. Ve a **Settings → Pages**. En *Source* elige **Deploy from a branch**, rama **main**, carpeta **/ (root)**, y toca **Save**.
5. En uno o dos minutos la app queda en `https://TU-USUARIO.github.io/bolsillo/`.

El código queda público, pero tus gastos no: esos nunca salen de tu celular.

**Otra opción:** entra a app.netlify.com/drop, arrastra esta carpeta y crea una cuenta gratis para que el sitio no se borre.

## 2. Instalarla en el celular

Abre tu enlace en **Chrome**. Luego ve a **Configuración → Instalar Bolsillo**, o usa el menú **⋮ → Instalar app**. En iPhone se hace desde **Safari: Compartir → Agregar a inicio**.

## 3. Pasar los datos que ya tienes en la versión de Claude

1. En la versión de Claude: **Configuración → Copiar copia de seguridad**.
2. En la versión instalada: **Restaurar copia** (aparece arriba mientras ves los datos de ejemplo, y también en Configuración). Pega la copia y confirma.

## 4. Que lea las notificaciones sola (Android)

Ve a **Configuración → Leer notificaciones solas (MacroDroid)**. La app te muestra los pasos y la dirección exacta que debes pegar en MacroDroid, ya con tu enlace.

## 5. Copias de seguridad

Como los datos viven en el celular, descarga de vez en cuando una copia en **Configuración → Descargar copia de seguridad** y guárdala en Drive. Si cambias de celular, la restauras allá.

## Actualizar la app

Si cambias `index.html`, sube el archivo nuevo al mismo repositorio. Para forzar que el celular descargue todo de nuevo, cambia en `sw.js` la línea `const V='bolsillo-v1'` por `bolsillo-v2`.
