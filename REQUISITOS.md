# Soldado y Coketa — Web (Ingeniería Web, E1)

Documento vivo de requisitos, decisiones y tareas pendientes. Se va actualizando
a medida que avanza el proyecto — tanto aquí como en el chat de Claude, como
trabajando con Claude Code sobre este mismo repositorio.

---

## 1. Qué es esto

Trabajo de la asignatura **Ingeniería Web** (entrega E1). El sitio es, a la
vez, el prototipo real de portfolio/tienda para la marca de ropa
**@soldadoycoketa** (Instagram), con la creadora de la marca dando feedback
sobre diseño y assets.

Dos objetivos en tensión, y hay que servir a los dos:

1. **Aprobar con nota alta** según la rúbrica formal del profesor (ver §3).
2. **Que el sitio tenga buena pinta de verdad** para la marca (referencias:
   namedcollective.com, bbesita.com, littlewebsite.co).

La solución de compromiso ya aplicada: una capa base "de clase" (evaluable)
+ una capa opcional `iag.css` con los efectos vistosos (ver §4).

---

## 2. Estado actual del repositorio

```
index.html          Inicio (hero + desfile de looks + manifiesto)
lookbook.html        Lookbook (vídeo + portfolio de fotos reales)
tienda.html           Tienda (catálogo, cómo hacer un encargo, guía de
                      tallas y 2 formularios)
css/
  variables.css       Colores, tipografías, reset box-sizing (común)
  headerfooter.css     Header + footer, EN UN SOLO FICHERO (común)
  inicio.css          Base evaluable de index.html
  lookbook.css        Base evaluable de lookbook.html
  tienda.css           Base evaluable de tienda.html (incluye el
                       "checkbox hack" del pedido, sin JavaScript)
  iag.css             Capa OPCIONAL/no evaluable (ver §4)
assets/
  logo-soldado-coketa.png, tangas.png, textura-rosa.png,
  modelo-1..11.png, pole-silhouettes.png
  lookbook/foto-01..22.jpg   Fotos reales de la colección (redimensionadas
                             a partir de wetransfer_img_0221-jpeg_.../)
```

Validado por última vez (antes de la reestructuración de esta sesión) con
el checker oficial de W3C (`vnu.jar`): **0 errores en los 3 HTML y en los
5 CSS evaluables.** **Pendiente**: revalidar tras los cambios de esta
sesión — `vnu.jar`/`html5validator` necesita Java, que no está instalado
en esta máquina y requiere `sudo` (contraseña) para instalarlo, así que
de momento solo se ha revisado a mano (balance de etiquetas, ids únicos).
Si validas con Java instalado y sale algo, dímelo. Sí se ha comprobado
con Playwright que no hay scroll horizontal ni imágenes rotas en
desktop/tablet/móvil, con y sin `iag.css`, y que el flujo de "añadir al
pedido" de la tienda funciona con ratón y con teclado.

El fichero `iag.css` da: hero fijo tipo namedcollective.com en Inicio
(el contenido sube y tapa el hero), barra de pole que recorre toda la
página, texturas en `mix-blend-mode`, y el desfile de Inicio animado en
bucle (como tenía antes el carrusel del lookbook), que se detiene al
pasar el ratón para poder ver bien el look ampliado. Si se quita
ese `<link>` del `<head>`, las 3 páginas se siguen viendo completas y
ordenadas (desfile como fila estática con hover simple, hero en el flujo
normal de la página, sin hueco de vídeo visible).

---

## 3. Rúbrica oficial (resumen)

- Mínimo 3, máximo 4 páginas, navegables con enlaces relativos.
- Estructura común (al menos header + footer) — **CSS de header/footer en UN
  SOLO fichero** (`headerfooter.css`). ✅ hecho.
- Usar todos los elementos HTML vistos en clase, correctamente.
- Usar selectores de clase, id y tipo donde corresponda.
- **Todos los ficheros deben pasar la validación real de
  validator.w3.org.** ⚠️ verificado antes de la reestructuración del
  22-23/09; **hay que revalidar** la versión actual (ver §5).
- Entrega: zip `IW-<DNI>-E1.zip` con el prototipo completo.
- Aviso explícito contra el uso excesivo de IA generativa.
- Válvula de escape explícita del enunciado: *"Si se quiere añadir
  animaciones o estilo muy diferente al visto en clase usando IAg, generar
  un iag.css (no evaluable)"*. ✅ aplicado.
- Penaliza: estructura HTML incorrecta, CSS no separado en ficheros o mal
  enlazado en `<head>`, código sin cerrar/errores, código sin comentar o sin
  indentar.
- Indicadores de nota: formularios con ≥6 tipos de elemento distintos,
  inputs específicos (email/password/number/date), imágenes con
  width/max-width + alt, enlaces relativos que funcionen, elementos
  semánticos HTML5, pseudo-clases en al menos un tipo de elemento, media
  query para una resolución concreta, bloques bien diferenciados (bordes/
  fondos), márgenes internos/externos, contenido real suficiente, botones/
  enlaces con estilo consistente, footer con info útil.

---

## 4. Lo visto en clase vs. lo que NO — repaso de las diapositivas del profesor

Leí las 7 presentaciones que has subido al proyecto. Esto es importante
porque el propio enunciado separa "visto en clase" (evaluable) de "con IA"
(en `iag.css`, no evaluable) — así que conviene saber exactamente dónde está
esa línea según ESTE profesor, no en general.

### SÍ está en las diapositivas (evaluable con total seguridad)

**HTML**: estructura del documento (`<!DOCTYPE>`, `<head>`, `<body>`),
`<meta charset>`, `<title>`, `<meta description>`, `<link>` favicon/css,
`<script>`; títulos `h1`-`h6`, `<p>`, `<br>`, `<hr>`, `<strong>`, `<em>`;
listas `<ul>`/`<ol>`/`<li>` (incluye anidadas); imágenes (`src`, `alt`,
`width`, `height`); tablas (`<tr>`, `<th>`, `<td>`, `colspan`, `rowspan`,
`<thead>`/`<tbody>`/`<tfoot>`); enlaces internos/externos, `target`, anclas
`#id`; comentarios `<!-- -->`; `<div>`/`<span>`. Semántico HTML5: `<header>`,
`<nav>`, `<main>`, `<aside>`, `<footer>`, `<article>`, `<section>` (con las
reglas de anidado que dan en la práctica 4: cada sección puede tener su
propio header/footer, un `<article>` puede contener varios `<section>`).
Formularios: `<form action method>`, `<input>` de tipo `text`, `password`,
`checkbox`, `radio`, `submit`; atributos `name`, `value`, `disabled`,
`required`, `autofocus`; `<select>`/`<option>`/`<optgroup>` (`multiple`,
`size`, `selected`); `<textarea>` (`rows`, `cols`, `maxlength`,
`minlength`); `<label for>`; `<fieldset>`/`<legend>`.

**CSS**: cómo aplicar CSS (inline/interna/externa, con la externa como la
recomendada); reglas CSS (selector/propiedad/valor), combinar selectores
con coma; selectores de **tipo, clase e id** (justo los 3 que pide la
rúbrica); comentarios; colores (`red`, `rgb()`, `#hex`); unidades (`px`,
`pt`, `em`, `rem`, `%`, palabras clave); propiedades de texto
(`font-family`, `font-size`, `font-weight`, `font-style`, `text-align`,
`line-height`); modelo de cajas (`border`, `padding`, `margin`, valor
`auto`); pseudo-clases (`:hover`, `:disabled`, `:required`, `:checked`,
selectores de atributo tipo `input[type="checkbox"]:checked`);
especificidad y herencia; propiedades abreviadas; `display` (`inline`,
`inline-block`, `block`, `none`); `float` (`left`/`right`/`both`/`none`).

**Responsive**: mobile first, imágenes adaptables (`max-width:100%`),
viewport meta, **media queries** (`min-width`/`max-width`), la alternativa
de `<link media="...">`. **Flexbox confirmado por el profesor** (visto en
clase; incluso comentó que es probablemente lo que usaría una IA para
maquetar páginas, por ser lo más útil) — el uso intensivo de `display:flex`
en las 3 páginas es 100% seguro.

**Accesibilidad**: `label for/id`, `alt` en imágenes, `<html lang="es">`,
elementos semánticos, accesibilidad por teclado.

### NO aparece en ningún resumen (riesgo → posible "no visto en clase")

Esto es lo importante: nuestro CSS base (el que se supone 100% evaluable)
usa varias técnicas que **no salen en ninguna de las 7 diapositivas**:

- ~~Custom properties / variables CSS~~ — **confirmado directamente por el
  profesor: permitido usarlo así.**
- `position: sticky` (header), `position: relative`/`absolute` — el temario
  de diseño de página no menciona `position` en absoluto, solo `display` y
  `float`.
- `clamp()` para tipografía fluida.
- `box-sizing: border-box` (reset global que añadí para evitar overflow).
- ~~Flexbox~~ — **confirmado por el profesor, visto en clase.**
- `transition` en los `:hover` (el profesor sí da `:hover`, pero no
  `transition`).
- `tbody tr:nth-child(even)` — pseudo-clase de uso muy estándar, pero
  tampoco sale explícitamente en el resumen (solo salen `:hover`,
  `:disabled`, `:required`, `:checked`).

**No es necesariamente un problema** — son todo técnicas CSS3 estándar y
muy básicas (no son "estilo generado con IA" en ningún sentido real), y es
muy probable que el profesor las dé por sabidas o las haya explicado en
clase sin que quedara en las diapositivas resumen. Pero como el propio
enunciado traza la línea en "lo visto en clase", merece la pena que decidas
tú cómo de estricto quieres ser. Opciones, de más a menos conservadora:

1. **Sustituir variables CSS por valores repetidos literalmente** (sin
   `:root`/`var()`) en los ficheros base, y dejar `variables.css` con los
   valores documentados como referencia/comentario. Mueve `position`,
   `clamp()`, `transition` a alternativas más "de clase" donde se pueda.
2. **Quedarnos como está** pero añadir un comentario al principio de cada
   `.css` explicando qué técnicas "extra" se usan y por qué (transparencia
   en vez de ocultarlo).
3. **Preguntar directamente al profesor** si las variables CSS y
   `position` cuentan como "visto en clase" antes de tocar nada — es la
   opción más segura y la más rápida.

👉 **Decidido: opción 2** (ver §5). Ojo: la nota de `variables.css`
todavía tiene 3 `#TODO` sin explicar (position, transition,
nth-child) — hay que completarlos antes de entregar.

---

## 5. Pendiente / TODO

- [x] Decidir qué hacer con las técnicas CSS no confirmadas en el temario
      (§4). **Decisión: opción 2** — se mantiene el CSS tal cual (var(),
      position, clamp(), box-sizing:border-box, transition, nth-child)
      y se añadió un comentario en `variables.css` (nota completa) y uno
      corto en cada uno de los otros 4 ficheros evaluables señalando qué
      técnicas "extra" usa cada uno. Cambio solo de comentarios, no afecta
      a la validación W3C ya hecha.
- [x] DNI y compresión final del zip — las hace el usuario, fuera de este
      flujo.
- [x] Flexbox confirmado por el profesor como visto en clase.
- [x] **Vídeo fijo en Lookbook, efecto namedcollective.com** (sesión
      2026-09-23): el vídeo de la colección ahora se comporta igual que
      el hero de Inicio — se queda pegado a la pantalla (`position:fixed`)
      mientras el resto de la página (intro, portfolio, guía de tallas)
      sube y lo tapa. Solo en `iag.css` (sin estampado, a diferencia del
      hero): nuevo `<div class="lookbook-video-spacer">` antes de la
      sección del vídeo (mismo patrón que `.hero-spacer` en Inicio), y
      `.intro`/`.portfolio`/`.tallas-section` llevan fondo sólido en
      `lookbook.css` para poder taparlo. Sin `iag.css` sigue siendo un
      bloque de vídeo normal en el flujo de la página. Verificado con
      Playwright: el vídeo permanece fijo mientras se hace scroll, y el
      portfolio lo tapa por completo al llegar a él, en desktop y móvil.
- [x] **Quitado el texto "Look N" del desfile de Inicio** (sesión
      2026-09-23): a petición del usuario, las 11 tarjetas del
      carrusel ya no llevan `<figcaption>`, solo el PNG. Se quitó
      también la regla `.fit-card figcaption` de `inicio.css` (sin uso).
- [x] **Logo grande y tangas del hero en unidades relativas, y bug de
      selección de texto en el carrusel** (sesión 2026-09-23):
      `.hero__logo`/`.hero__tangas` en `index.html` pasan de
      `width`/`height` en px (HTML y CSS) a `max-height` (25vh/14vh) +
      `max-width` (70vw/45vw) + `width:auto;height:auto` en
      `inicio.css`. **Ojo**: se probó primero con `height` fijo en vh
      (como pedías) y también con `aspect-ratio` añadido encima, y
      ambas variantes deformaban el logo en móvil vertical (el
      `max-width` en vw recorta el ancho pero no reescala el alto fijo).
      La combinación `max-height` + `max-width` + auto en las dos
      dimensiones sí mantiene la proporción real (1.414) en todos los
      anchos probados. **Texto "Look XX" superpuesto a las fotos del
      carrusel — diagnóstico corregido**: mi primer diagnóstico (caja
      azul de selección de texto) era incorrecto; se dejó igualmente
      `user-select:none` en `.fit-card` porque no está de más en una
      cinta animada, pero no era la causa real. **El bug de verdad**:
      `.desfile__lista` hereda de `inicio.css` un `max-width:1300px`
      (pensado para el modo cuadrícula sin `iag.css`), y `iag.css` no lo
      anulaba al activar el modo cinta (`flex-wrap:nowrap`). Con
      `nowrap` las 22 tarjetas no pueden bajar de línea, así que se
      encogían para caber en esos 1300px — pero las imágenes tienen
      `width:220px` fijo y no se encogen con ellas, así que se
      solapaban unas con otras, y el `figcaption` de una tarjeta
      terminaba pintado encima de la foto de la vecina. Solución:
      `max-width: none;` en la regla de `.desfile__lista` de `iag.css`.
      Verificado con Playwright en varias posiciones de la animación
      (looks 01 a 11): imágenes separadas, sin solapes.
- [x] **Logo del header como imagen** (sesión 2026-09-22): el
      `header__logo-link` de las 3 páginas pasó de texto ("SOLDADO Y
      COKETA") a `<img src="assets/logo-header.png">`, sin width/height
      en el HTML — el tamaño se fija en `headerfooter.css` con unidades
      relativas (`height:4vh` en la imagen). **Bug encontrado y
      corregido**: poner `max-width:40%` directamente en la imagen crea
      una referencia circular (el ancho máximo se calcula sobre el
      ancho de `.header__logo-link`, que a su vez se ajusta al ancho de
      la imagen) y el logo se renderizaba deformado a ~3px de ancho.
      Solución: el `max-width:40%` va en `.header__logo-link` (que sí
      tiene un ancho de referencia claro, el de `.header__nav-row`), y
      la imagen lleva `max-width:100%` en su lugar — mismo resultado
      visual pretendido (tope de seguridad en pantallas muy bajas/
      anchas) sin la circularidad. Verificado con Playwright: logo a
      36×36px en desktop y 33,8×33,8px en móvil, idéntico en las 3
      páginas, sin scroll horizontal con ni sin `iag.css`.
- [x] **Reestructuración de las 3 páginas** (sesión 2026-09-22):
      Inicio pasa de "3 destacados en tarjeta gris" a un desfile de los
      11 looks con fondo transparente; con `iag.css` es una cinta
      animada en bucle (como tenía antes el carrusel del lookbook) que
      se pausa y amplía el look al pasar el ratón por encima (sin
      vídeo, solo hover). Lookbook pierde el carrusel animado de
      `modelo-N.png` y "cuidados de la prenda"; gana un vídeo grande
      (sin estampado) + un portfolio con las 22 fotos reales de
      `wetransfer_img_0221-jpeg_.../`; mantiene la guía de tallas.
      Tienda pasa de tabla a tarjetas de producto (catálogo
      placeholder) con insignias, y el formulario de encargo suma una
      lista de "prendas seleccionadas" que se rellena marcando las
      tarjetas — **sin JavaScript**, con la técnica CSS "checkbox
      hack" (`:checked` + combinador `~`). Detalle completo en
      `/home/rubba/.claude/plans/atomic-seeking-journal.md`.

### Pendiente (revisado 2026-09-28)

**Bloqueante para la entrega** (la rúbrica lo penaliza directamente):

- [x] **Revalidado HTML/CSS** (2026-09-28, tras los cambios de ese día)
      contra los servicios online de validator.w3.org/nu y
      jigsaw.w3.org/css-validator: 0 errores en los 3 HTML y en los 5
      CSS evaluables. Repetirlo si se cambia algo antes de entregar.
- [x] **Completados los 3 `#TODO` de `variables.css`** (2026-09-28):
      explicación de `position`, `transition` y `nth-child`, más una de
      `columns` (nuevo mosaico del portfolio). Conviene que los repases
      con tus palabras, porque están escritos en primera persona.
- [x] **`<h1>` en Inicio** (2026-09-28): el logo del hero va dentro de
      `<h1 class="hero__titulo">` (con `alt="Soldado y Coketa"`), con los
      márgenes del h1 a 0 en `inicio.css`. Se ve exactamente igual: logo
      a 283×200 en desktop y 262×185 en móvil, con su proporción real.
- [x] **Las prendas del catálogo ahora sí se envían con el encargo**
      (2026-09-28): los 5 `.prod-check` llevan `name="prendas"`,
      `value` y `form="form-encargo"`, así que pertenecen al formulario
      aunque sigan fuera de él (necesario para el checkbox hack).
      Comprobado con Playwright que se marcan, se ven en la lista y
      aparecen en los datos del formulario.
- [x] **Favicon** (2026-09-28): `<link rel="icon">` con
      `logo-header.png` en las 3 páginas.
- [x] Indentado el `<ul>` de `<nav class="footer__social">` en las 3
      páginas (2026-09-28).

**Contenido (depende de la marca/usuario):**

- [ ] **Vídeo pendiente de añadir** (la estructura ya está lista, solo
      falta el archivo): `assets/videos/lookbook-reel.mp4`, comentado
      dentro del `<video>` de `lookbook.html`. Mientras no esté, con
      `iag.css` el Lookbook dedica una pantalla entera (100vh fija) a un
      póster con controles que no reproducen nada. Si el vídeo no llega
      a tiempo, mejor quitar `controls` o sustituir el `<video>` por la
      foto de portada.
- [x] **Catálogo de Tienda con los 10 diseños reales** (2026-09-30):
      ya están en la web ADVERTISEMENTS, EXMAQUINA, FOR BIGBOYS, Kate's
      on crack!!, MOST HATED, MSGA, Ojos de ángel, PLAYGIRL, REVEAL y
      XPERT, cada uno con su foto, nombre, checkbox, línea en el pedido y
      reglas `:checked`. Sin descripción. Precios y etiquetas de la
      dueña: 25,99 € (ADVERTISEMENTS, Kate's on crack!!, MOST HATED,
      MSGA, PLAYGIRL, XPERT) y 23,99 € (EXMAQUINA, FOR BIGBOYS, Ojos de
      ángel, REVEAL). Etiquetas: "Explicit", "Cunty", "Extra Cunty", y
      Ojos de ángel lleva dos ("Anuel AA" y "Cunty"). Las etiquetas van
      dentro de `.producto__badges`, que las apila en la esquina.
      Validado en W3C (2026-09-30, subido a mano): `tienda.html` da 0
      errores y 0 avisos. Solo salen mensajes "Info" por la barra final
      de las etiquetas vacías (`<img … />`, `<br />`), que pone Prettier
      al formatear. No son errores y no afectan. El CSS también está
      validado. Las fotos, en `assets/tienda/<nombre>.png`, están
      recortadas a 480 px de ancho y los nombres de fichero no llevan
      espacios ni tildes (1,2 MB en total, antes 8 MB). Los A4
      originales quedaron fuera del repo, en `../assets-originales/tienda/`.
      Las fotos de la tarjeta se ven enteras (`object-fit: contain`, 180
      px de alto). Probado con Playwright: las 10 cargan, se
      añaden y quitan, y se envían con el formulario.
      Antes: **Catálogo de Tienda con los diseños reales**: de momento son 5
      placeholders (Camiseta Actitud, Sudadera Calle, Pack Tangas, Top
      Noche, Conjunto Coketa) con fotos reutilizadas de `modelo-4..8.png`
      (looks de desfile, no fotos de producto real). **Falta que el
      usuario pase la lista de diseños** (nombre, precio, descripción,
      foto y talla/s de cada uno). Al cambiarlos hay que tocar, por cada
      prenda: la tarjeta del catálogo, su checkbox `#prod-x` (`value`), su
      línea en `.lista-pedido` y los 4 bloques de reglas `:checked` de
      `tienda.css` (borde, botón, textos, línea del pedido). Si cambia el
      número de prendas, añadir o quitar un selector en cada bloque.
- [x] Texto de la "Guía de tallas" con tono divertido (2026-09-29, hecho
      por el usuario; ahora se rehace entera, ver pedidos del 29/09).
- [ ] Decidir si el pole-strip debe notarse *menos* agresivo (quedó
      pendiente de validar con la creadora de la marca).

**Pedidos del equipo (2026-09-28):**

- [x] **Logo y tangas del hero más grandes** (2026-09-28): logo de
      `25vh`/`70vw` a `35vh`/`85vw`, tangas de `14vh`/`45vw` a
      `20vh`/`60vw`, sin `height` fijo. ⚠️ Falta comprobarlo en móvil
      vertical.
- [~] **Textos de la dueña de la marca** (2026-09-29, en curso):
      - ✅ Inicio: manifiesto nuevo y valores ("Diseño único", "Tiradas
        exclusivas", "Sexy & Cunty"). Se quitó el eslogan del hero ("Sin
        filtros, sin permiso"), que sigue como título del manifiesto.
      - ✅ Lookbook: intro nueva.
      - ✅ Comentarios nuevos en el `<head>` y el header de `index.html`.
      - Tienda (decidido 2026-09-29):
        - ✅ El `<aside>` "Cómo hacer un encargo" y los textos de los
          formularios **se quedan como están**.
        - [ ] Intro de la Tienda: se cambia, pero el texto está por
          pensar.
        - [ ] **Productos sin descripción**: cada tarjeta solo lleva
          nombre y precio (quitar el `<p>` de descripción de los 5
          `<article class="producto">`; la regla `.producto p` de
          `tienda.css` sigue haciendo falta para el precio).
        - [x] **Etiquetas rosas**: ahora "Explicit", "Cunty", "Extra Cunty" y
          "Anuel AA" (ver catálogo).
      - Limpieza pendiente: la regla `.hero__eslogan` de `inicio.css` e
        `iag.css` ya no tiene uso desde que se quitó el eslogan.
- [x] **Email de contacto real** `soldadoycoketa@gmail.com` en el footer
      de las 3 páginas (2026-09-29; el usuario lo cambió en Inicio y se
      aplicó igual en Lookbook y Tienda).
- [x] **Copyright "SoldadoYCoketa"** en `.footer__copy` de las 3
      páginas (2026-09-28). `.footer__brand` se queda como estaba
      ("SOLDADO Y COKETA"): falta decidir si también cambia.
- [x] **Portfolio del Lookbook en mosaico** (2026-09-28): `columns: 4
      220px` con cada foto en su proporción real (las verticales ya no
      salen recortadas), con 1 de cada 3 fotos desplazada 2rem hacia
      abajo para romper la alineación. En móvil (≤640px) pasa a 2
      columnas sin desplazamiento. ⚠️ Falta verlo en el navegador.
- [x] **Botón "Añadir al pedido" ↔ "Quitar del pedido"** con colores
      invertidos al marcar la prenda (2026-09-28, ver §6).

**Pedidos del equipo (2026-09-29):**

- [x] **Tangas del hero más grandes** (2026-09-30): `.hero__tangas`
      de `20vh`/`60vw` a `30vh`/`80vw`. Comprobado: 381×270 px en
      escritorio y 311×220 en móvil vertical, sin scroll horizontal y
      con el botón "Ir a la tienda" dentro de la pantalla.
- [x] **Logo y tangas un poco más grandes y más juntos** (2026-09-30):
      el hueco grande entre ellos venía de los **bordes transparentes de
      los PNG** (en `tangas.png` solo 170 de 707 px de alto eran
      tangas). Se recortaron las dos imágenes a su contenido, dejando
      10 px de margen: `tangas.png` pasa a 877×190 y
      `logo-soldado-coketa.png` a 1355×640. Los originales están en el
      historial de git. Como ahora el tamaño en CSS es el tamaño visible,
      los topes cambian: logo `26vh`/`90vw`, tangas `9vh`/`85vw`, y el
      `gap` de `.hero__lockup` pasa a `2.5rem`. Resultado en escritorio:
      logo 495×234 y tangas 373×81 (antes, a la vista, unos 445×197 y
      327×65), con unos 40 px entre ellos en vez de unos 160. Visto
      también en móvil vertical y horizontal, sin scroll lateral.
- [x] **Collage del Lookbook sobre el vídeo, sin fondo negro**
      (2026-09-30, hecho en `iag.css`: `.portfolio` con fondo
      transparente, sombra en el título "La colección" y en las fotos).
      Comprobado en escritorio y móvil, sin scroll lateral. Mientras no
      llegue el vídeo, detrás se ve el póster (`foto-01.jpg`), que
      también es la primera foto del collage: saldrá repetida hasta
      entonces. Una de las fotos del collage (4.ª columna en escritorio,
      la del bosque) se ve **girada 90°**: revisarlo al elegir las fotos
      nuevas. Pedido original: Que las
      fotos del portfolio se vean flotando encima del vídeo fijo. Hay que
      quitar el `background-color` negro de `.portfolio` en
      `lookbook.css` (está ahí justo para tapar el vídeo con `iag.css`).
      Ojo: **sin `iag.css`** el vídeo no es fijo, así que en la capa base
      el portfolio seguirá sobre fondo negro, y eso está bien. Revisar
      que el título "La colección" se lea sobre el vídeo (sombra de
      texto o una franja detrás) y que el portfolio sin fondo no deje
      ver el vídeo en huecos raros del resto de la página. Mientras no
      llegue el vídeo real, lo que se verá detrás es el póster
      (`foto-01.jpg`).
- [x] **Guía de tallas movida del Lookbook a la Tienda** (2026-09-30, hecho;
      queda debajo de "Cómo hacer un encargo") y cambiar su
      contenido: ya no son medidas en cm sino 3 tallas "con actitud".
      Texto de la dueña, tal cual:

      > **(XS) XtraSlut**
      > Para lxs que queréis mostrar el precioso cuerpo con el que Dios
      > os trajo al mundo, sexys y atrevidxs
      >
      > **(M) Medium Slut**
      > Not to innocent and not too much, para lxs que quieren ser más
      > misteriosos y no perder la picardía
      >
      > **(XL) Xtra Large Slut**
      > Para lxs que estáis más feeling yourself con el EXTREME Oversize,
      > divertido, extra cómodo y extracunty

      Cómo quedó: tabla de 2 columnas (Talla | Para quién), con el nombre
      en la primera columna con `<br>` ("XS<br>XtraSlut"). Se mantienen
      el `caption` y el `tfoot` del usuario. Los estilos pasaron de
      `lookbook.css` a `tienda.css`, se quitó `.tallas-section` de
      `iag.css`, y los radios del formulario son ahora XS, M (marcada) y
      XL. Validado en W3C y visto en escritorio y móvil. ⚠️ El texto va
      tal cual lo pasó la dueña: "Not **to** innocent" probablemente
      debería ser "too". El `caption` dice "excepto las de tienda", y
      ahora la tabla está en la tienda: revisar si se entiende.

      Notas que se tomaron para hacerlo:
      - Mantenerla como `<table>` (suma puntos: `thead`/`tbody`/`tfoot`,
        `colspan`, `caption`) con 2 columnas: Talla | Para quién. Sin la
        columna de cadera en cm.
      - Mover también sus estilos (`table`, `caption`, `th/td`,
        `thead th`, `tbody tr:nth-child(even)`, `tfoot td`,
        `.tallas-section`) de `lookbook.css` a `tienda.css`.
      - Quitar `.tallas-section` de `iag.css` (lista del vídeo fijo) si
        ya no está en Lookbook.
      - Sitio natural en Tienda: después del catálogo o junto al
        `<aside>`.
      - **Las tallas del formulario de encargo** (radios XS/S/M/L/XL)
        pasan a ser solo XS, M y XL para que cuadren con la guía.
      - Decidir si se mantienen el `caption` y el `tfoot` que escribió el
        usuario ("estas tallas no son reales…", "coge con la que más
        muestres ;)").
      - Actualizar los enlaces y el texto que mencionen "tallas" en el
        Lookbook (descripción `<meta>`, comentarios).
- [ ] **Otras fotos y otro orden en el collage del Lookbook.** El
      usuario elige cuáles y en qué orden. Hoy son las 22 de
      `assets/lookbook/foto-01..22.jpg` en orden numérico. Al cambiarlas,
      el `width`/`height` de cada `<img>` debe ser la proporción real de
      esa foto (el mosaico respeta la proporción de cada una), y hay que
      actualizar los `alt`. Fotos nuevas: redimensionarlas antes (las
      actuales van a 1600 px de lado largo).
- [x] **Ventana emergente "Parental Advisory"** (2026-09-30, hecho en
      Inicio, solo HTML y CSS). Aparece **cada vez que se carga
      `index.html`** como una ventanita (caja negra de 380 px como
      máximo, con borde rosa y el logo a 260 px) sobre la página
      oscurecida. Con `iag.css` el fondo además sale desenfocado
      (`backdrop-filter: blur(8px)`). Imagen:
      `assets/LogoVentanaEmergente.png`, recortada del A4 original a
      1016×618. El original quedó fuera del repo, en
      `../LogoVentanaEmergente-original.png`.
      - **"Me atrevo!!"** es el `<label>` de `#aviso-check` (checkbox
        oculto con `autofocus`), y `#aviso-check:checked ~ .aviso {
        display: none; }` la cierra. Es el mismo "checkbox hack" de la
        tienda y suma `autofocus`, visto en clase y sin usar hasta ahora.
      - **"Soy aburridx:("** es un enlace a `https://www.google.com`.
        Cambiar el destino si se prefiere otro.
      - Estilos en `inicio.css` (`.aviso…`), con `z-index: 1000` para
        quedar por encima de la barra de pole.
      - Comprobado con Playwright: se cierra con ratón y con teclado
        (espacio nada más entrar, Tab pasa a "Soy aburridx:("), tapa
        header y pole, y cabe en escritorio, móvil vertical y móvil
        horizontal. Validado en W3C.
      - Limitaciones sin JavaScript: vuelve a salir cada vez que se
        vuelve a Inicio (también desde el menú), y con Tab se puede
        llegar a los enlaces de detrás aunque no se vean. Solo en
        Lookbook y Tienda no sale; para ponerla también ahí, copiar el
        bloque del `<body>` y las reglas `.aviso…` a sus CSS.

      Pedido original:
      una capa a pantalla completa con la imagen de Parental Advisory
      (la tiene el usuario; guardarla en `assets/`) y **dos botones**.
      Por decidir:
      - **Qué dicen y qué hacen los dos botones.** Por ejemplo: "Entrar"
        cierra el aviso, y "Salir" lleva fuera de la web.
      - **Si sale solo en Inicio o en las 3 páginas**, y si sale en cada
        visita o solo la primera vez.

      Cómo hacerlo según la respuesta:
      - **Solo con HTML y CSS** (evaluable, sin JavaScript): capa fija
        encima de todo que se cierra con el mismo "checkbox hack" de la
        tienda (el botón "Entrar" es un `<label>` de un checkbox oculto,
        y `:checked ~ .aviso { display: none; }`). El botón de salir es
        un enlace normal. Limitación: el aviso vuelve a salir cada vez
        que se carga la página, también al navegar entre páginas, así
        que conviene ponerlo **solo en Inicio**.
      - **Que salga solo la primera vez**: necesita JavaScript +
        `localStorage` para recordar que ya se aceptó (igual que el modo
        "clienta"), en un `.js` aparte.
      - Accesibilidad: el aviso tiene que poder cerrarse con teclado, y
        mientras está abierto no debería poder tabularse a la página de
        detrás.
- [ ] **Cambiar los diseños de la Tienda** por los reales: ver
      "Catálogo de Tienda con los diseños reales" arriba. Pendiente de
      que el usuario pase la lista.

**Extra (pedido 2026-09-28, no entra en la rúbrica):**

- [ ] **Tienda en modo "clienta" tras el acceso.** Al entrar por "Acceso
      clientas", la página de la tienda cambia:
      - Un saludo arriba del todo según el email con el que se ha
        entrado (p. ej. "Hola, maria@…").
      - El formulario de encargo ya no pide "Nombre completo" ni
        "Email": se dan por conocidos por la sesión y se envían solos,
        sin que se vean en el formulario.

      ⚠️ Esto no se puede hacer solo con HTML y CSS, porque la página
      tiene que recordar quién ha entrado. Opciones, de más sencilla a
      más completa:
      1. **JavaScript + `localStorage`** (sin servidor, vale para GitHub
         Pages): al enviar el acceso se guarda el email; la tienda lo lee,
         pinta el saludo y quita esos campos del formulario. No hay login
         de verdad (no se comprueba la contraseña), es solo una simulación.
         Iría en un `.js` aparte, como `iag.css`, para no mezclarlo con la
         parte evaluable.
      2. **Backend real** (servidor, base de datos, sesiones): login de
         verdad, pero se sale del alcance de la asignatura y de GitHub
         Pages.

      Sin JavaScript activo, la tienda tiene que seguir funcionando igual
      que ahora (con los campos de nombre y email visibles).

**Opcional (suma puntos en "usar todos los elementos vistos en clase"):**

- [x] **`<aside>` en Tienda** (2026-09-28): "Cómo hacer un encargo",
      entre el catálogo y los formularios, con un `<ol>` de 3 pasos y un
      `<strong>`. Estilo en `.como-funciona` de `tienda.css`. Es texto
      provisional: entra en la lista de textos que reescribe la dueña.
- [x] **`<tfoot>` + `colspan`** en la guía de tallas (2026-09-28): "Si
      estás entre dos tallas, coge la mayor."
- [ ] Siguen sin usarse: `<em>`, `<hr>`, `<br>`, `rowspan`,
      `<optgroup>`. Ninguno es obligatorio.

---

## 5b. Estado frente a la rúbrica (revisión 2026-09-28)

| Criterio | Estado | Dónde |
|---|---|---|
| 3-4 páginas con enlaces relativos | ✅ 3 páginas | header + footer |
| Header/footer comunes, CSS en un solo fichero | ✅ | `headerfooter.css` |
| CSS separado y enlazado en `<head>` | ✅ | 6 ficheros |
| Selectores de tipo, clase e id | ✅ comentados como tales | `headerfooter.css` |
| Formulario con ≥6 tipos de elemento | ✅ text, email, date, number, radio, checkbox, password, select, textarea, fieldset/legend | `tienda.html` |
| Imágenes con width/max-width + alt | ✅ todas | las 3 |
| Semántico HTML5 | ✅ header, nav, main, section, article, aside, figure, footer | |
| Pseudo-clases | ✅ :hover, :focus-visible, :checked, :nth-child | |
| Media query | ✅ `max-width: 640px` en los 4 CSS de página | |
| Bloques diferenciados, márgenes, botones consistentes | ✅ | |
| Footer con info útil | ✅ redes, newsletter, contacto, copyright | |
| Validación W3C | ✅ 0 errores (28/09) | §5 |
| Código comentado | ✅ | |
| `<h1>` por página | ✅ (en Inicio, el logo del hero) | |
| Página correcta sin `iag.css` | ✅ comprobado con Playwright (22-23/09) | |

## 6. Ideas / backlog de diseño (ir añadiendo aquí)

Mejoras encontradas en la revisión del 2026-09-28, de más a menos útil:

- ✅ **Botón "Añadir al pedido" ↔ "Quitar del pedido"** (2026-09-28):
  al marcar una prenda, el botón invierte sus colores (fondo negro, texto
  rosa) y cambia de texto, sin JavaScript. El label lleva los dos textos
  en `<span>` y `:checked ~ …` muestra solo el que toca. Comprobado con
  Playwright en escritorio y móvil, y validado en W3C.
- **Los 5 "Añadir al pedido" suenan igual en lector de pantalla** (mismo
  texto para 5 checkboxes). Añadir el nombre de la prenda en un `<span>`
  oculto visualmente, p. ej. "Añadir al pedido <span>Camiseta
  Actitud</span>".
- **Peso de imágenes**: `assets/` son 13 MB. `textura-rosa.png` pesa
  2,3 MB (se ve con opacidad baja, sirve igual un JPG/WebP de ~200 KB),
  `logo-header.png` es de 2239×2239 px para mostrarse a ~36 px, y los
  `modelo-N.png` rondan 400 KB cada uno (22 cargas en Inicio con
  `iag.css`, aunque se repitan los ficheros). Añadir
  `loading="lazy"` a las 22 fotos del portfolio también ayuda.
- **CSS repetido entre páginas**: la regla `body {…}` está idéntica en
  `inicio.css`, `lookbook.css` y `tienda.css`, y `.intro` igual en
  lookbook y tienda. Se podría mover `body` a `variables.css` (que ya
  cargan las 3). No es obligatorio: tener cada página autocontenida
  también es defendible.
- **`--alto-header: 7vh`** es una estimación: el header real (ticker +
  nav) mide lo que marcan su padding y fuente, no 7vh, así que el
  pole-strip puede empezar un poco solapado o separado del header según
  la pantalla. Solo afecta a `iag.css`.
- **`prefers-reduced-motion` del ticker está duplicado** en
  `headerfooter.css` e `iag.css`. Se puede quitar el de `iag.css`.
- Logo del header a `height: 4vh`: en móvil en horizontal (poca altura)
  se queda muy pequeño. Un `min-height: 28px` lo evita.

## 7. Preguntas abiertas

- ¿Llega el vídeo del lookbook antes de la entrega? Si no, decidir qué
  hacer con el hueco (ver §5).
- ¿Hay fotos/precios reales para la tienda o se entrega con los
  placeholders? (29/09: se cambian; falta la lista de diseños.)
- Intro de la Tienda y texto de las insignias rosas: por pensar.
- Aviso "Parental Advisory": ¿"Soy aburridx:(" debe llevar a Google
  o a otro sitio? ¿Solo en Inicio (como ahora) o en las 3 páginas?
- Qué fotos del Lookbook y en qué orden.


*Última actualización: 2026-09-30 (tangas más grandes y guía de tallas en
Tienda). 2026-09-29: Textos de la dueña (en curso) y pedidos del 29/09 en §5. Antes, 2026-09-28: revisión completa de las 3 páginas y
los 6 CSS: estado frente a la rúbrica (§5b), pendientes (§5) y mejoras
(§6).*
