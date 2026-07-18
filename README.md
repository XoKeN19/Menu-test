# El Pollito de Arica — Menú digital editable

Menú de restaurante 100% estático (HTML/CSS/JS, sin backend) que se publica en
**GitHub Pages** y se edita desde un panel de administración protegido.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | Menú público que ven los clientes. Lee los datos de `menu.json`. |
| `admin.html` | Panel de administración para editar y **publicar** el menú. |
| `menu.json` | Los datos del menú (categorías y platos). **Fuente de la verdad.** |

## Cómo funciona

- `index.html` carga `menu.json` cada vez que alguien abre el menú, así todos ven
  siempre la última versión.
- `admin.html` permite editar el menú y, al pulsar **Publicar en GitHub**, guarda
  los cambios directamente en `menu.json` del repositorio usando la API de GitHub.
- Los cambios se guardan también como *borrador* local (en el navegador) mientras
  editas; **Publicar** es lo que los hace visibles para todos.

## Seguridad y privacidad

- Para **publicar** hace falta un **token de acceso de GitHub** con permiso de
  escritura sobre este repositorio. Sin un token válido nadie puede cambiar el menú:
  la autorización la valida GitHub, no el navegador.
- El token **nunca** se guarda en el repositorio. Se almacena solo en el navegador
  del administrador (en este dispositivo). Puedes quitarlo con el botón
  "Conectado → Desconectar".
- El menú de un restaurante es público por naturaleza, así que el repositorio puede
  ser público sin problema. Nadie sin token puede modificarlo.

## Puesta en marcha (una sola vez)

### 1. Activar GitHub Pages
1. En GitHub: **Settings → Pages**.
2. En *Source* elige la rama `main` y carpeta `/ (root)`. Guarda.
3. Tu menú quedará en `https://XoKeN19.github.io/Menu-test/` y el panel en
   `https://XoKeN19.github.io/Menu-test/admin.html`.

### 2. Crear un token fino (fine-grained PAT)
1. Ve a **https://github.com/settings/personal-access-tokens/new**.
2. *Resource owner*: tu usuario. *Repository access*: **Only select repositories →
   `Menu-test`**.
3. *Permissions → Repository permissions → Contents*: **Read and write**.
4. Genera el token y cópialo (empieza con `github_pat_...`). Guárdalo en un lugar
   seguro; GitHub solo lo muestra una vez.

### 3. Usar el panel
1. Abre `admin.html` (la URL de Pages de arriba).
2. Pega tu token y pulsa **Conectar y entrar**.
3. Edita categorías/platos y pulsa **Publicar en GitHub**.
4. Espera ~1 minuto (lo que tarda GitHub Pages en actualizar) y recarga el menú.

### Subir tus propias imágenes
Al editar un plato o una categoría verás el botón **"Subir imagen…"**. Elige una
foto desde tu teléfono o computador: se optimiza (se reduce de tamaño) y se sube a
la carpeta `images/` del repositorio con tu mismo token. La imagen queda enlazada
al plato automáticamente. También puedes seguir pegando una URL si lo prefieres.
Recuerda pulsar **Publicar en GitHub** para que los cambios se vean en el menú.

### Mostrar u ocultar platos (sin borrarlos)
Cada categoría funciona como **acordeón** y muestra **todos** tus platos, incluidos
los que no aparecen en el menú. Junto a cada plato hay un botón de ojo 👁:
- 👁 (verde) = el plato **se muestra** en el menú.
- 🚫 (gris) = el plato está **oculto** (se ve atenuado con "Oculto" en el panel,
  pero **no** aparece en el menú público).

Con un clic lo enciendes o apagas. El contador de cada categoría muestra
`visibles/total`. Así puedes tener un catálogo de platos y elegir cuáles se
muestran sin tener que recrearlos. Recuerda **Publicar en GitHub** para aplicar.

> Si prefieres solo ver/editar sin publicar, usa "Entrar solo en modo local".

## Si haces un *fork* del repo

Edita las constantes al inicio del `<script>` de `admin.html`:

```js
const GH = { owner: 'TU_USUARIO', repo: 'TU_REPO', branch: 'main', path: 'menu.json' };
```
