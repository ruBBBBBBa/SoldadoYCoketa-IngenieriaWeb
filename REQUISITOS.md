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
lookbook.html        Lookbook (vídeo + portfolio de fotos reales + tallas)
tienda.html           Tienda (catálogo en tarjetas + 2 formularios)
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
  validator.w3.org.** ✅ verificado en local con el checker oficial.
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

👉 **Pendiente de decidir contigo.** Mi recomendación es la 3 si hay
margen de tiempo, si no la 2.

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
- [ ] **Vídeo pendiente de añadir** (la estructura ya está lista, solo
      falta el archivo): 1 vídeo de colección en Lookbook
      (`assets/videos/lookbook-reel.mp4`, comentado dentro del
      `<video>` de `lookbook.html`). Inicio ya no lleva vídeo por look
      (se descartó esa idea, ver más arriba).
- [ ] **Catálogo de Tienda con productos reales**: de momento son 5
      placeholders (Camiseta Actitud, Sudadera Calle, Pack Tangas, Top
      Noche, Conjunto Coketa) con fotos reutilizadas de `modelo-4..8.png`
      (looks de desfile, no fotos de producto real) — sustituir nombres,
      precios, descripciones y fotos cuando estén disponibles.
- [ ] Reescribir el texto de la tabla de "Guía de tallas" en lookbook con
      tono "divertido" (lo hace el usuario).
- [ ] Decidir si merece la pena añadir un `<aside>` en alguna página
      (el profesor lo explica con detalle en la práctica 4 y no lo hemos
      usado todavía en ninguna página).
- [ ] Revisar comentarios e indentación del código fuente final — la
      rúbrica penaliza "código sin comentar o sin indentar" explícitamente.
- [ ] Revalidar HTML/CSS con `vnu.jar` en cuanto haya Java instalado
      (ver §2) — de momento solo revisión manual tras la reestructuración.
- [ ] Decidir si el pole-strip debe notarse *menos* agresivo (quedó
      pendiente de validar con la creadora de la marca).

## 6. Ideas / backlog de diseño (ir añadiendo aquí)

  

## 7. Preguntas abiertas

- (vacío por ahora)


*Última actualización: generado automáticamente al reconstruir la web
según la rúbrica formal (ver historial de chat para más detalle).*
