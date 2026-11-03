# Plantilla «Fisioterapia y osteopatía» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **dinámico**
(azul petróleo + naranja quemado + blanco roto; bandas a todo el ancho que entran cortadas en diagonal sobre la
anterior; titulares en mayúsculas condensadas y pesadas; botones, etiquetas e iconos en paralelogramo; fotos a sangre
con un borde en diagonal y un trazo naranja inclinado en la portada). Todo en castellano de España, frases cortas,
tono directo y cercano, sin jerga clínica. Nunca hables de cómo está hecha la web.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa (listas propias `tratamientos` y `bonos`); no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = petróleo de bandas, cabecera y pie; acento = naranja de botones, trazos y bono destacado; fondo = blanco roto; texto = casi negro). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…). Los derivados (`--hondo`, `--quemado`, `--claro`, `--linea`, `--suave`) se calculan con `color-mix` en `src/styles/global.css`.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-titulos` condensada del sistema, `--d` altura del corte diagonal, `--inclinacion`, bandas `.banda-fondo/.banda-clara/.banda-petroleo/.banda-honda/.banda-quemada` + `.oscura`, botones `.btn`/`.btn-sec`/`.btn-claro`/`.btn-petroleo`, cabecera `.cabecera--dinamico`, pie `.pie--dinamico`). El corte diagonal lo pone el CSS a todas las secciones menos la primera, alternando el sentido: no hace falta tocar nada al reordenar. Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (se generan aparte a partir de `fotos.json`); las de respaldo en `public/placeholders/`. En `site.yaml` con ruta absoluta (`/fotos/hero.jpg`). Las personas usan `/placeholders/persona.svg` hasta que el cliente suba su foto: **no se generan caras**.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = trazo naranja con una articulación + nombre.
- **Cabecera**: fija a todo el ancho, siempre sólida. Botón = `site.yaml → boton_cabecera`.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones (en este orden en el ejemplo)
Cada sección es un componente que solo se pinta si `secciones.<id>.activa` es `true`, en el orden de `site.yaml`. Un apartado nuevo puede reutilizar un diseño con `tipo: <id>`.
- `hero` → portada con `imagen` a sangre, velo petróleo, `antetitulo`, `titulo`, `texto`, `cta`, `cta_secundario` y franja naranja inclinada con `items: [{titulo, texto, icono}]`.
- `cifras` → banda petróleo con `items: [{titulo (la cifra), texto}]`. Sin cifras no se pinta.
- `tratamientos` → `tratamientos: [{nombre, texto, duracion, modalidad, precio}]` (modalidad «Presencial», «A domicilio» o «Presencial y a domicilio»), `imagen` como franja de foto a sangre y `cta`.
- `dolencias` → banda naranja con `items: [{titulo, texto, icono}]` e `imagen` (50/50).
- `proceso` (Método) → pasos `items: [{titulo, texto, icono}]` numerados e `imagen` (50/50, foto a la izquierda).
- `bonos` → `bonos: [{nombre, precio, sesiones, incluye («;»), destacado}]` y `cta` (botón de cada bono).
- `equipo` → `personas: [{nombre, cargo, foto, texto}]` y `galeria` (franja de fotos de borde a borde).
- `opiniones` → `testimonios: [{texto, autor, nota}]` sobre `imagen` con velo.
- `preguntas` → `preguntas: [{pregunta, respuesta}]` en acordeón.
- `cita` → 50/50: pasos `items: [{titulo, texto}]`, `cta`, `enlace_agenda` + `texto_agenda`, `nota`, `boton` y formulario (tratamientos y modalidades salen de `tratamientos`).
- `contacto` → datos de `contacto`, `imagen` y `boton` (si no hay `cita`, el formulario va aquí).
- `texto` (`tipo: texto`) → apartado genérico con `texto`, `declaracion`, `items`, `imagen` y `cta`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Para varios valores, una cadena separada por «;» (`incluye` de los bonos).
5. **No inventes** precios, opiniones, cifras, colegiaciones ni datos clínicos: si el cliente no los da, deja el campo vacío o la lista vacía; el componente lo oculta.
6. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
7. **Sección nueva**: mejor un id nuevo con `tipo:` (`texto`, `tratamientos`, `dolencias`, `proceso`…). Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y bandas a todo el ancho. `src/pages/index.astro` la recoge sola.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto (`.contenedor`, `--gutter`), bandas y fotos de borde a borde, sin scroll horizontal en móvil, ids `hero` y `contacto`. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altGaleria`, `altSeccion`, `altFicha`, o el nombre de la persona); las decorativas, `alt=""`.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.tratamientos.tratamientos` → `/tratamientos/<slug>/` (tratamiento).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/tratamientos/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
