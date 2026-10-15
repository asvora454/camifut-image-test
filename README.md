# CAMIFUT: diagnóstico de tres imágenes en GitHub Pages

Este directorio es un experimento **independiente**. Contiene únicamente `index.html`, este README y `.nojekyll`; no incluye catálogo, aplicación, fotografías descargadas, credenciales ni datos de clientes. `.nojekyll` impide que Jekyll procese el HTML plano. **Nada se ha publicado.**

## Publicación manual futura — requiere autorización previa

1. Confirmar que se acepta que el sitio de prueba será **público**. Según [GitHub Docs](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site), las páginas son accesibles públicamente incluso si el repositorio fuese privado en un plan que admita Pages privado; en GitHub Free, Pages requiere un repositorio público. No añadir información sensible.
2. En la cuenta personal de GitHub, comprobar primero si ya existe `camifut-image-test`. Si existe, revisar su contenido y no sobrescribirlo. Si no existe, crear **un repositorio separado** con ese nombre exacto, sin vincularlo al repositorio de CAMIFUT. Para GitHub Free, elegir visibilidad pública; no activar dominio personalizado.
3. Tras autorizar expresamente la publicación, subir **solo** `index.html`, `README.md` y `.nojekyll` de esta carpeta a la raíz de `main`. No subir `catalog-data.js`, `app.js`, `deploy/`, `camifut-hostinger.zip` ni la carpeta de Python. La interfaz de GitHub pedirá guardar los archivos en un commit; ese paso **no se ha realizado**.
4. En el repositorio de prueba: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: main → Folder: /(root) → Save**. Esperar a que Pages confirme la URL. La ruta esperada tiene la forma `https://<usuario>.github.io/camifut-image-test/`; no se ha creado ni verificado una URL real. [Instrucciones oficiales de GitHub](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
5. Abrir la URL final en Chrome y comprobar que la propia página declara `protocolo: https:`. No modificar DNS ni asociar `camifut.es`.

## Comprobación de las tres imágenes

El HTML tiene exactamente tres etiquetas `<img>` externas, apuntando a las URL originales de Porto, Argentina y Zaragoza en `photo.yupoo.com`. No usa proxy, `fetch`, `crossorigin`, `referrerpolicy` especial ni fallback. Una etiqueta `CARGA` solo cuenta como éxito si `naturalWidth > 0`; `FALLA` es un evento `error`. Un `responseStatus=0` de Resource Timing **no** es un código HTTP observado.

En Chrome, abrir DevTools (`F12`) **antes** de recargar, seleccionar **Network**, activar **Disable cache** y, si se desea conservar redirecciones, **Preserve log**. Filtrar por `photo.yupoo.com` o por tipo **Img** y recargar una sola vez. Para cada una de las tres filas anotar **Status**, Request URL, **Initiator**, Type/Content-Type, Server, Location/redirecciones y el mensaje de **Console**. Abrir cada fila y revisar **Headers**, **Initiator** y **Response/Preview**. No alterar cabeceras ni usar extensiones para cambiar la solicitud. [Guía oficial de Chrome DevTools](https://developer.chrome.com/docs/devtools/network).

| ID | Evento / ancho natural en Pages | HTTP real en Network | Content-Type / servidor / redirección |
| --- | --- | --- | --- |
| 258397373 (Porto) | Pendiente | Pendiente | Pendiente |
| 258395695 (Argentina) | Pendiente | Pendiente | Pendiente |
| 258369578 (Zaragoza) | Pendiente | Pendiente | Pendiente |

Comparar con la prueba local en `127.0.0.1`, donde las tres emitieron `error` y `naturalWidth=0`. Si cargan en Pages, eso solo demuestra funcionamiento en ese origen y momento; si fallan, HTTPS por sí solo no resuelve el problema. No afirmar éxito antes de ejecutar la prueba autorizada.
