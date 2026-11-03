# Plantilla NoExpertise · Fisioterapia y osteopatía

Web de una página para centros de fisioterapia, osteopatía, rehabilitación, podología y quiromasaje. Estilo
**dinámico**: azul petróleo, naranja quemado y blanco roto, bandas a todo el ancho cortadas en diagonal, titulares en
mayúsculas condensadas y fotos a sangre. Astro 5 + Tailwind 4, derivada de AstroWind (MIT).

Todo el contenido está en `site.yaml`. Ejemplo: «Elástica Fisioterapia», un centro ficticio de Jerez de la Frontera.

## Secciones y campos propios

| Sección | Qué enseña | Campos propios |
|---|---|---|
| `hero` | Portada con foto a sangre y franja de accesos | `items: [{titulo, texto, icono}]` |
| `cifras` | Banda de cifras | `items: [{titulo, texto}]` |
| `tratamientos` | Tratamientos con duración, modalidad y precio | `tratamientos: [{nombre, texto, duracion, modalidad, precio}]`, `imagen`, `cta` |
| `dolencias` | Lo que se trata (espalda, rodilla, deportiva…) | `items: [{titulo, texto, icono}]`, `imagen` |
| `proceso` | Método en pasos | `items: [{titulo, texto, icono}]`, `imagen` |
| `bonos` | Bonos de sesiones | `bonos: [{nombre, precio, sesiones, incluye, destacado}]`, `cta` |
| `equipo` | Fisioterapeutas y fotos del centro | `personas: [{nombre, cargo, foto, texto}]`, `galeria` |
| `opiniones` | Opiniones de pacientes | `testimonios: [{texto, autor, nota}]`, `imagen` |
| `preguntas` | Preguntas frecuentes | `preguntas: [{pregunta, respuesta}]` |
| `cita` | Pedir cita con formulario | `items: [{titulo, texto}]`, `cta`, `enlace_agenda`, `texto_agenda`, `nota`, `boton` |
| `contacto` | Datos de contacto y foto | `imagen`, `boton` |

`texto.astro` es el diseño genérico para apartados nuevos (`tipo: texto`).

## Construir

```
npm ci
npm run build    # dist/
```

Fotos: `fotos.json` (se generan aparte). Diseño: `DISEÑO.md`. Reglas para agentes: `CLAUDE.md`.

## Páginas propias
- Cada elemento de `secciones.tratamientos.tratamientos` con `detalle` tiene su página en `/tratamientos/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas`. Sin la clave, una sola página larga.
