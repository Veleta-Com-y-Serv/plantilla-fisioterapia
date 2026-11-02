# Fisioterapia y osteopatía: brief de diseño

Plantilla `fisioterapia` creada el 02/11/2026 a partir de `psicologia-terapia` (base de origen) con
`php artisan plantillas:nueva`. De la base solo queda la estructura técnica (`Base.astro`, `site.ts`, SEO de base,
formulario, `Imagen.astro`, filas 50/50); el diseño es otro. Tanda «ancho completo» 3, fila 2, orden 500.

## Brief

- **Para quién**: centros de fisioterapia, osteopatía, rehabilitación, podología y quiromasaje. Quien entra tiene dolor
  o una lesión y quiere saber si le pueden ayudar, cuánto cuesta y cuándo le dan cita.
- **Qué tiene que conseguir la web**: pedir cita (formulario, WhatsApp o teléfono), con bonos como segunda acción.
- **Tono y estilo** (`dinamico`): enérgico, claro, deportivo sin ser de gimnasio. Sí: carteles deportivos, señalética
  inclinada. No: la calma en arco y serif de `psicologia-terapia` ni las tarjetas blancas en caja centrada.
- **Concepto**: el movimiento en diagonal. Cada banda entra cortada en diagonal sobre la anterior (alternando el
  sentido; lo hace el CSS con `main > section:nth-child`), botones, etiquetas, iconos y números de paso en
  paralelogramo (`--inclinacion: -12deg`), fotos con el borde interior en diagonal, un trazo naranja inclinado que cruza
  la portada y otro bajo la franja de foto de tratamientos.
- **Paleta de ejemplo**: primario `#1f4e5a` (petróleo), acento `#d9692f` (naranja), fondo `#f6f1ea` (blanco roto),
  texto `#1b2326`. Derivados: `--hondo` (petróleo oscuro: cabecera, pie, bonos, opiniones), `--quemado` (naranja
  oscurecido para bandas con texto claro y contraste AA), `--claro` (petróleo al 9 % sobre el fondo).
- **Tipografía**: titulares en mayúsculas condensadas y pesadas (`Bahnschrift` con `font-stretch: 75%`, `DIN
  Condensed`, `Roboto Condensed`, `Arial Narrow`); texto en `system-ui`. Portada 3-7 rem.
- **Ritmo de bandas**: portada (foto + velo) → cifras (petróleo) → tratamientos (blanco roto + franja de foto) →
  dolencias (naranja, 50/50) → método (petróleo claro, 50/50) → bonos (petróleo hondo) → equipo (blanco roto +
  mosaico) → opiniones (foto + velo) → preguntas (blanco roto) → cita (naranja | petróleo claro) → contacto (50/50) →
  pie (petróleo hondo con el nombre enorme).
- **Apartados y listas propias**: `tratamientos` (nombre, texto, duracion, modalidad, precio), `dolencias.items`,
  `proceso.items`, `bonos` (nombre, precio, sesiones, incluye, destacado), `equipo.personas` + `galeria`,
  `opiniones.testimonios`, `preguntas`, `cita`, `contacto`, `cifras.items`.
- **Fotos** (`fotos.json`, 10): sala con camilla (portada), bodegón de material (franja), manos sobre espalda y
  ejercicio de rodilla (sin caras), box, sala de ejercicio, material, recepción, pasillo con paralelas, fachada en
  Jerez. Sin texto legible, sin logotipos, sin personas reconocibles.
- **Qué no hacer**: arcos, serif ligera, colores salvia, cabecera transparente, tarjetas blancas; tampoco la mudanza en
  cursiva de `transporte-mudanzas` (allí el título va en cursiva pesada; aquí recto y condensado).
