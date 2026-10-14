# Inventario Veraile — Fase 0 (solo lectura)

Fecha: 2026-10-14 · Sitio: **Veraile Inmobiliaria** (`61f9d3408efe602f155341f0`, workspace `6224eb33e2f1f81739ba3990`) · Dominios: `veraile.com`, `www.veraile.com`.

> Es el sitio de **producción**. No se ha editado ni publicado nada. Único cambio: la página "Testing area" (`6acf3d5d1e943fcc9142ffeb`) puesta en borrador para que no se publique.
> Sitios hermanos en el mismo workspace: "Veraileinmobiliaria's SLIDER" (`6418f4aea6f538aa72b098b9`) y "Clone" (`655e8b147a39ae6bc745b31d`, 2023).

## Páginas (18)

| Página | Slug | Notas |
|---|---|---|
| Home | `/` | editada hoy 08:28 |
| Inmuebles | `/inmuebles` | listado con filtros (clases `c-filtros*`) |
| Inmuebles Madrid | `/inmuebles-madrid` | variante del listado |
| Inmuebles Copia | `/inmuebles-copia` | copia de 2023, candidata a limpiar |
| Servicios | `/servicios` | |
| Política de Privacidad | `/politica-de-privacidad` | |
| Search Results | `/search` | |
| 404 | `/404` | |
| Test Page | `/test-page` | de 2022, publicada |
| Style Guide | `/settings-and-info/style-guide` | heredada de plantilla Biznus |
| Order Confirmation / Checkout / Checkout (PayPal) | | heredadas de plantilla ecommerce, sin uso aparente |
| Plantillas CMS | | Inmuebles Template (`/product`), Categories Template (`/category`), Alert Bar Template (`/alert`), SKUs Template (`/sku`) |
| **Testing area** | `/testing-area` | creada hoy, **borrador** |

## CMS (4 colecciones)

| Colección | ID | Fichas |
|---|---|---|
| **Inmuebles** | `62045eaf439d8c7b1c669130` | **213** |
| SKUs | `62045eaf439d8c22a866912f` | 213 (1 por inmueble) |
| Categories | `62045eaf439d8c3e76669131` | 4 |
| Alert Bar | `62045eaf439d8cdaf266912e` | 1 |

### Inmuebles: campos

| Campo (slug) | Tipo | Notas |
|---|---|---|
| name, slug | Texto | obligatorios |
| `regimen-2` "Régimen" | Opción | Alquiler / Venta (obligatorio) |
| `ubicacion` "Dirección" | Opción (18) | en realidad es el **pueblo**: Aldeanueva, Collado, Cuacos de Yuste, Garganta la Olla, Jaraíz, Jarandilla, Losar, Madrigal, Pasarón, Talaveruela, Torremenga, Valverde, Viandar, Villanueva, Madrid, Arroyomolinos, Valdeíñigos de Tiétar, Tejeda de Tiétar |
| `localizacion` | Texto | calle/dirección libre |
| `tipo-de-inmueble` | Texto libre | "Piso, Casa, Local…" (no es lista) |
| `m2` | Texto | |
| `habitaciones`, `banos` | Número | |
| `parking`, `terraza`, `ascensor`, `a-c`, `piscina` | Interruptor | |
| `vendido-alquilado` "Vendido/Alquilado/Reservado" | Opción | Vendido / Alquilado / Reservado; vacío = disponible |
| `precio-especial` | Texto | para > 999.999 € o "CONSULTAR PRECIO" |
| `featured` "Inmueble destacado" | Interruptor | |
| `full-description` | Texto enriquecido | |
| `category` | Multi-referencia | Categories (Alquiler, etc.) |
| `default-sku` | Referencia | SKUs: **aquí están precio y fotos** |
| Restos ecommerce | | `sku-properties`, `shippable`, `tax-category`, `ec-product-type`, `description` |

### SKUs: campos relevantes

- `price` (EUR, en céntimos: `6900000` = 69.000 €), **`compare-at-price`**, `main-image`, `more-images` (galería). El resto (peso, medidas, suscripción…) es ecommerce sin uso.

### Recuento por estado (213 fichas)

| Estado | Fichas |
|---|---|
| Vendido | 93 |
| Alquilado | 7 |
| Reservado | 6 |
| Disponible (sin estado) | 107 |
| Régimen Venta / Alquiler | 204 / 9 |

Hay fichas archivadas (por ejemplo `casa-en-jaraiz-de-la-vera-23`).

## Estilos

- **811 estilos**: 626 clases, 176 combo, 9 etiquetas (ninguno de librería).
- Convención propia `c-*`: `c-card`, `c-card_image`, `c-card_content`, `c-card_price`, `c-card_place`, `c-card_type`, `c-card_extras`, `c-filtros*`, `c-img-gallery*`, `c-detail*`, etc.
- Restos de plantilla Biznus (`Hero*`, `Cards*`, `Pill`, `Price Wrapper`, `color-block`, …).
- Variables de estilo: **pendiente** de leer.

## Componentes (6)

| Componente | Instancias |
|---|---|
| Nav | 6 |
| NavBar_2 | 5 |
| Nav Bar2 | 0 (sin uso) |
| Footer | 11 |
| Inmuebles form | 1 |
| Cookie Banner | 0 (sin uso) |

Nota: hay dos navegaciones en uso (Nav y NavBar_2).

## Scripts y código

- Scripts registrados: **ninguno**. Scripts aplicados vía API: ninguno.
- Código libre en cabecera (sitio): **Elfsight** (widget, `platform.js`) y **Iubenda** (consentimiento de cookies). Pie: vacío.
- Finsweet no está instalado.

## Hallazgos para la prueba piloto (tarjetas con estados)

1. **Rebajado**: no existe campo. Pero SKUs ya tiene **`compare-at-price`**, que puede hacer de "Precio anterior" sin crear campos nuevos (comprobar si alguna ficha lo usa).
2. **Nuevo**: no hay campo. Se puede deducir de la fecha de creación (`createdOn`) con un script, o crear un interruptor "Es nuevo".
3. **Reservado / Vendido**: ya existe `vendido-alquilado`. 93 vendidos dan material de sobra para "Últimas ventas".
4. **Pueblo**: ya existe como opción (`ubicacion`, 18 valores), aunque se llama "Dirección".
5. **Tipo**: texto libre; normalizarlo exigiría un campo nuevo de lista.
6. El precio vive en SKUs, no en Inmuebles: hay que tenerlo en cuenta al conectar las tarjetas.

## Home: estructura (lectura)

Orden real de secciones: `Nav` (componente) → `Hero Section` (`#Hero`) → sección `Inmuebles` (bloque CTA + `#Ultimos-inmuebles` con lista CMS `Products List Wrapper`, versión escritorio) → otro `Container mobile oportunidades` (lista CMS para móvil) → `Oportunidades` (tercera lista CMS) → `Servicios` → `Contacto` (columnas + formulario) → `Footer` (componente).

- Hay **3 listas CMS de inmuebles** en la Home, y los tres bloques comparten `id="Ultimos-inmuebles"` (id repetido; conviene corregirlo en staging).
- Los bloques "Recién llegados" y "Últimas ventas" del plan se corresponden con estas listas; falta abrir cada lista para ver sus filtros y la tarjeta (`c-card*`).

## Variables de estilo

Una sola colección, `default` (modo base). No hay variables de marca definidas: colores y tipografías están puestos directamente en las clases.

## `compare-at-price`

No se puede filtrar por campos de tipo Precio vía API, así que no sé cuántas fichas lo usan. Se puede comprobar leyendo SKUs por tandas o mirando en el Designer.

## Piloto de tarjetas con estados (página borrador "Testing area", `6acf3d5d1e943fcc9142ffeb`)

Hecho el 2026-10-14. Solo en esa página (borrador) + clases `test-*` nuevas. Nada publicado.

**Creado**
- 10 clases `test-*`: `test-grid`, `test-card`, `test-card_photo`, `test-card_body`, `test-card_title`, `test-card_place`, `test-badge`, `test-price`, `test-price-old`, `test-price-drop`.
- 4 tarjetas de muestra estáticas (Nuevo, Rebajado, Reservado, Vendido) con `data-estado`.
- CSS de estados en el código de cabecera **de la página** (selectores `[data-estado]` / `[data-badge]`).
- Script `VerailePilotEstados` v0.0.1, aplicado solo a la página: calcula `data-estado` desde `data-cms-estado`, `data-cms-old` y `data-cms-created`.
- Collection List sobre Inmuebles (límite 6) con una tarjeta: título (Name), pueblo (Dirección) y `data-cms-estado` (Vendido/Alquilado/Reservado) ya enlazados.

**Salió solo (API)**: clases, estructura, estados por CSS, script, lista de colección y enlaces de texto/atributo de campos propios de Inmuebles.

**Hubo que retocar / no es posible por API**
- `set_text` en el builder no se guardó (quedó el texto de relleno); se corrigió con `set_settings`.
- **No son enlazables por API**: `price` y `compare-at-price` (tipo Precio, en SKUs) y la fecha de creación. Hay que enlazarlos a mano en el Designer: precio → `test-price`, `compare-at-price` → atributo `data-cms-old`, fecha de creación → atributo `data-cms-created`. Sin ellos no salen Nuevo ni Rebajado en la lista real.
- Falta la foto: enlazar `Default SKU › Main Image` al fondo/imagen de `test-card_photo`.
- Orden de la lista: pendiente de poner "más recientes primero" (la ordenación no se probó).

## Staging (copia segura)

- **Copy of Veraile Inmobiliaria** · siteId `6acf46c079e13ee0a6bfb366` · workspace `6257473c3e5c610181b2812d` (el de Andrés) · sin dominios propios.
- Verificado 2026-10-14: 19 páginas, 4 colecciones, 213 fichas, scripts `VerailePilotEstados` y `VerailePilotHome` y el CSS del piloto.
- Publicado solo en `https://veraile-7c607b9967c33f0f5a3cf013cbc1fe6.webflow.io` (páginas `/home-2-0-borrador` y `/testing-area`, sacadas de borrador **solo en la copia**).
- Producción (`61f9d3408efe602f155341f0`, workspace `6224eb33e2f1f81739ba3990`) queda solo para lectura. Las páginas de prueba que creé allí siguen en borrador.
- Desde ahora, toda escritura va al staging.

## Fase 1 en el staging (`6acf46c079e13ee0a6bfb366`, colección Inmuebles `6acf46c079e13ee0a6bfb352`)

Solo añadido, nada borrado ni rellenado todavía:
- `Es nuevo` (interruptor, con ayuda) · `Publicar en redes` (interruptor, con ayuda).
- `Tipo` (lista: Piso, Casa, Chalet, Finca, Local comercial, Edificio, Solar, Nave, Ático, Otro). El texto libre "Tipo de inmueble" se conserva.
- Ya existían y se reutilizan: estado (`vendido-alquilado`), pueblo (`ubicacion`, llamado "Dirección") y precio anterior (`compare-at-price` en SKUs).
- Recuento aproximado por texto de "Tipo de inmueble": Casa 71, Piso 58, Finca 39, Local 15, Solar 10, Chalet 7, Edificio 5, Nave 2, Ático 2, sin tipo 2.
- Pendiente de OK de Andrés: muestra de 10 fichas para rellenar `Tipo` y `Es nuevo`.

Limitaciones de la API en la copia: escribir el código de cabecera de una página da 404 y los scripts copiados no se pueden editar (se registró `VerailePilotHomeB`).

## Home 2.0 en el staging: estados según maqueta (2026-10-14)

- Página `home-2-0-borrador` (`6acf46c079e13ee0a6bfb34a`) en el staging. Script `VerailePilotHomeC` v0.0.1 (el anterior no se podía editar en la copia).
- Pastillas como en `Home.html`: Nuevo (blanca con punto turquesa), Precio rebajado (turquesa, flecha) + cajita con los euros rebajados, Reservado (oscura translúcida), Vendido (gris + "✓ Vendido" abajo a la izquierda). Se ocultan las etiquetas antiguas `c-card_type` (VENTA/OPORTUNIDAD) solo en esa página.
- "Es nuevo" no se puede enlazar a un atributo; se enlaza la **visibilidad** de un marcador `data-flag="nuevo"` dentro de la tarjeta (el script lo detecta).
- Comprobado en la web publicada: 4 Nuevo, 4 Vendido, 1 Rebajado.
- Pendiente: el diseño de la tarjeta (foto 280 px, precio 24 px arriba, "4 hab. · 2 baños · 238 m²") todavía es el de la web actual; hay que restilar `c-card*` (en el staging se pueden editar las clases reales).

## Paso 1 y 2 en el staging: tarjeta, hero y buscador (2026-10-14)

- Tarjeta (`c-card*`, `Shop Item Price`, `Shop Item Name`) restilada como la maqueta; el combo `c-card_content.home` tenía `min-height:180px` (causa del hueco). Cambios hechos sobre las clases reales **de la copia**.
- Sección: eyebrow "Disponibles", H2 "Recién llegados", enlace "Ver todos los disponibles".
- Hero: tarjeta redondeada 600 px con margen 96 px, titular "Casas, fincas y negocios en La Vera", sin botón; eyebrow `v2-eyebrow` nueva.
- Buscador (HtmlEmbed bajo el hero, GET a `/inmuebles`): Operación (`tipo=Venta|Alquiler`), Tipo (`tipoinmueble`), Pueblo (`pueblo`), Precio máximo (`preciomax`).
- Comprobado: el listado de la copia acepta filtros por URL (`?tipo=Venta` → 192 de 199; `?Tipo=Alquiler` → 7). **Solo Operación es funcional hoy**; Tipo, Pueblo y Precio máximo necesitan campos de filtro en las tarjetas y el formulario de `/inmuebles`.
- Limitación API: publicar a una web ya publicada exige esperar 1 minuto entre publicaciones.

## Home 2.0 en el staging: secciones completas (2026-10-14)

Página `home-2-0-borrador` (`6acf46c079e13ee0a6bfb34a`), publicada solo en el subdominio de la copia.
- Cabecera (componente `Nav`, en la copia): Comprar, Alquilar, Vender tu casa, Pueblos, Últimas ventas + botón con el teléfono (WhatsApp). Los enlaces antiguos (tipo página) se sustituyeron por enlaces URL con filtro (`/inmuebles?tipo=Venta|Alquiler`) y anclas (`/#Contacto`, `/#pueblos`, `/#ventas`).
- Hero, buscador (solo Operación filtra de verdad), franja de cifras, Recién llegados (6 fichas, pastillas de estado).
- **Últimas ventas**: la 3.ª lista de la Home (y su versión móvil) filtradas por `Vendido`, 4 fichas, fondo menta, fotos en gris y "✓ Vendido". El precio y los iconos se ocultan por CSS en esa sección.
- Busca por pueblo (enlaces a `/inmuebles?pueblo=...`, aún sin efecto) + Valorar mi casa (ancla a `#Contacto`) + formulario de contacto existente + oficinas. El componente `Footer` se quitó solo de esta página; el pie nuevo lleva las dos oficinas.
- Pendiente: filtros Tipo/Pueblo/Precio en `/inmuebles`; texto en vez de iconos en la fila de datos; ocultar "m²" vacío; ficha de inmueble; móvil a repasar con capturas.

## Fase 1 aplicada en el staging: tipos de inmueble (2026-10-14)

- Colección nueva **Tipos de inmueble** (`6acf660a3f67d08e25b7bf2b`): Casa, Piso, Finca, Local comercial, Solar, Edificio, Chalet, Nave, Ático, Otro.
- Campo nuevo `tipos` (referencia múltiple) en Inmuebles, además de `tipo` (opción, **tipo principal**, una sola) y `es-nuevo` (interruptor).
- Rellenadas las **213** fichas (en 5 tandas de ≤50). Tipo principal: Casa 66, Piso 58, Finca 40, Local comercial 15, Solar 12, Edificio 7, Chalet 6, Nave 3, Ático 2, Otro 4. **16 fichas con más de un tipo** (p. ej. Finca + Casa, Casa + Local comercial).
- Regla: el primer sustantivo del texto actual de "Tipo de inmueble" (o del nombre si estaba vacío) es el principal; los demás tipos que aparezcan se añaden a `tipos`. "Dúplex" solo = Piso; "Plaza de garaje", "Fábrica" y "Complejo rural" = Otro.
- `es-nuevo` = true en las 7 fichas creadas en los últimos 30 días. `publicar-en-redes` sin rellenar (decisión del cliente).
- Verificado tras escribir: 0 fichas sin `tipos`; recuentos de Casa (66), Finca (40) y Nuevo (7) coinciden.
- Producción: sin cambios. Estos campos solo existen en la copia.

## Filtros de /inmuebles aplicados en el staging (2026-10-14)
- Staging `6acf46c079e13ee0a6bfb366` (copia, no producción). Publicado solo a su subdominio .webflow.io.
- No se puede enlazar una lista anidada al multi-referencia `Tipos` por API, así que cada tarjeta lleva un bloque oculto (`[data-v2=filtros]`) con 3 textos: `pueblo` (←Dirección), `tipoinmueble` (←Tipo) y `tipoinmueble` (←campo nuevo "Tipos (texto para filtro)").
- Campo nuevo `Tipos (texto para filtro)` (PlainText, slug `tipos-texto-para-filtro`): relleno en las 213 fichas con los nombres de `Tipos` separados por coma. Opcional: solo hace falta para fichas con más de un tipo; el tipo principal sale de `Tipo`.
- Formulario del filtro: nuevo HtmlEmbed con checkboxes Tipo de inmueble y Pueblo (`fs-cmsfilter-field`).
- Verificado en Playwright: `?tipoinmueble=Casa` 63, `Solar` 12, `?pueblo=Jaraíz de la Vera` 117, ambos 28, `?tipo=Venta&tipoinmueble=Finca` 38 (de 199 visibles).
- Pendiente: `preciomax` del buscador de la Home aún no filtra (el precio es texto).

## Ficha de inmueble rehecha en el staging (2026-10-14)
- Plantilla `Inmuebles Template` (`6acf46c079e13ee0a6bfb33d`) de la copia `6acf46c079e13ee0a6bfb366`. El bloque antiguo ("Content Section") queda OCULTO, no borrado.
- Nuevo bloque `[data-fx=sec]` con esqueleto (migas, píldoras Régimen/Tipo, título, ubicación, precio, galería 1+4, tarjetas hab./baños/m², descripción, chips, zona aproximada, panel de contacto). Los elementos con datos (precio SKU, nombre, galería, rich text, amenidades, formulario) se MOVIERON con `move_element`, así que conservan sus enlaces a CMS.
- Dos HtmlEmbed con CSS (escritorio/móvil/print) y uno con script: WhatsApp con mensaje prellenado, "Ver las N fotos", Ficha PDF (`window.print()`), Compartir (`navigator.share`/copiar enlace) y barra fija móvil (WhatsApp + Llamar).
- Verificado con Playwright en escritorio (1440) y móvil (390) sobre `/product/edificio-en-jaraiz-de-la-vera`.
- Pendiente: "También te puede interesar" (lista relacionada), miniaturas móviles, probar ficha con terraza/parking (chips) y vendido, revisar mapa/zona.

### Ficha: relacionados y estado (2026-10-14)
- "También te puede interesar": lista Inmuebles (100) con tarjeta enlazada; un script la reduce a 3 (mismo pueblo primero, sin la ficha actual) y construye el enlace desde un texto oculto con el Slug (la API no deja enlazar el enlace dinámico).
- Píldora de estado (Vendido/Alquilado/Reservado) enlazada al campo CMS en la cabecera.
- Verificado: ficha con terraza/parking/aire (chips), tarjetas 4 hab./2 baños/238 m², zona, relacionados; ficha reservada muestra "RESERVADO".

## Ajustes por feedback del cliente (2026-10-14, staging)
- Home 2.0: franja de cifras centrada; hero, buscador, bloques de pueblos/valoración, servicios y oficinas ceñidos a 1248 px centrados (oficinas ahora tarjeta redondeada, no ancho completo).
- Tarjetas (Home y /inmuebles): fila de datos en texto "3 hab. · 2 baños · 120 m²" (m² vía texto oculto enlazado al campo `m2`; si falta, no se muestra).
- Ficha: fotos con bordes redondeados y overlay "Ver las N fotos" cubriendo toda la baldosa; columna derecha más ancha (5/12); descripción con "Leer más"; formulario compactado.
- Ficha PDF (print CSS): una página A4 con foto principal + 3 fotos, tarjetas de datos, resumen (2 primeros párrafos), chips y bloque de contacto.
- Nota: el campo `m2` está relleno en ~81 de las primeras 100 fichas; donde falta no se muestra.

### Ajustes 2 (2026-10-14, staging)
- Home: cifras centradas (número sobre texto); "Busca por pueblo"/valoración, bloque de contacto/formulario y "Ven a vernos" alineados al mismo ancho (96→1344 a 1440 px) que el resto.
- Tarjetas (Home y /inmuebles): vuelven los iconos, pero SOLO si hay dato (hab., baños, m²; pin de ubicación solo si hay texto), m² en la misma fila, más aire inferior. Se eliminó el script de fila de texto; ahora es CSS (`:has(:empty)`), por eso funciona también en el Designer salvo la lógica de vacíos, que solo se ve publicada.

### Ajustes 3 (2026-10-14, staging)
- /inmuebles: hueco entre foto y precio eliminado (imagen de tarjeta a 220 px, `.c-card_image` ya no 280 con img 180).
- Destacado superior: pastilla blanca sólida con sombra y texto oscuro (antes semitransparente y ilegible); fila m²/baños alineada.
- Iconos de ubicación, habitaciones, baños y m²: SVG minimalistas (trazo fino) aplicados como máscara CSS sobre los `<img>` existentes (sin cambiar los activos). Mismo CSS en Home y /inmuebles.

### Ajustes 4 (2026-10-14, staging)
- /inmuebles: panel de filtros en acordeón unificado (Régimen, Habitaciones, Baños, Extras, Tipo de inmueble, Pueblo): cerrados por defecto, flecha, contador de selecciones y se abre solo el grupo con filtros activos (p. ej. al llegar desde la Home con `?pueblo=`). Script + CSS en el embed de override de la página.
- Ficha PDF: cabecera de marca (veraile · Inmobiliaria · La Vera + teléfono/email), título/precio, foto principal + 3 fotos, datos, resumen y pie de contacto; una sola página A4 (`@page margin:0` quita cabecera/pie del navegador); oculto el icono verde de iubenda en impresión.
- "También te puede interesar": miniatura del inmueble enlazada al campo imagen principal; tarjeta con foto + nombre + pueblo.

## Revisión de diseño y contenido + micro-animaciones (2026-10-14, staging)
- Correcciones: textos "¿Qué hacemos?" y "Viandar de la Vera (Cáceres)" (Home y ficha); contraste del subtítulo del formulario y del eyebrow del hero; fila de datos de tarjetas alineada a la izquierda y sin huecos (`min-height` de `.c-card_content.home` anulado); sección "Últimas ventas" sin hueco.
- Móvil Home: "Recién llegados" pasa a carrusel horizontal con snap; servicios con ilustraciones más pequeñas.
- Móvil /inmuebles: el panel de filtros era un cajón fuera de pantalla (`translateY(-536px)`) y dejaba un hueco; ahora botón "Filtros" que despliega el acordeón (abierto si hay parámetros en la URL).
- Ficha móvil: ubicación en una línea (se oculta el pueblo duplicado), icono de galería arriba a la derecha.
- Micro-animaciones (CSS + IntersectionObserver, respetan `prefers-reduced-motion`): entrada del hero y de la cabecera de la ficha; reveal escalonado al hacer scroll (tarjetas, servicios, bloques); hover con elevación y zoom suave de foto en tarjetas; hover en chips de pueblo, botones, tarjetas de oficina, galería y relacionados; foco del buscador; pulso del botón WhatsApp; contador animado de las cifras (+100, 15).
- Embeds de pulido por página: Home `167d6330…` y `ba83bde1…`; /inmuebles `f4c7dfb8…` y `7c2186cd…`; ficha `8bdc8d21…`.
- Pendiente: filtro de precio máximo del buscador; cualquier cambio de copy/imágenes final con el cliente.
