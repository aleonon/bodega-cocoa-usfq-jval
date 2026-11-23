# DESIGN.md — Bodega COCOA

> **Sistema de diseño del frontend · Desarrollo Web 3 · USFQ**  
> **Versión:** 1.0 · 22 de noviembre de 2026  
> **Equipo:** Juanes Vargas y Ailyn León  
> **Fuente visual:** [`docs/diseno/brand-board.html`](docs/diseno/brand-board.html), basado en `brand-board-bodega-cocoa-v2.html` y el moodboard del equipo.  
> **Fuente funcional:** [`docs/prd/prd.md`](docs/prd/prd.md).  
> **Estado:** guía de diseño para el MVP; decisiones técnicas visuales sujetas a validación con el equipo.

**Lee este archivo antes de crear o modificar cualquier pantalla.** El PRD define qué hace el producto y sus reglas; este archivo define cómo se presenta y se comporta visualmente. Si una especificación funcional contradice este documento, prevalece el PRD: corregir el diseño y actualizar ambos documentos en el mismo cambio. **No inventar una regla de negocio para justificar una decisión visual.**

## 1. Concepto

**Less friction. More creation.** Bodega COCOA es una plataforma de reserva de equipos y espacios audiovisuales que combina el carácter de una publicación editorial con la claridad de un catálogo digital y la precisión de una herramienta de operaciones.

**Tres palabras clave:** editorial · preciso · elegante.

**Dirección:** *Editorial Creative Commerce*, con tipografía contundente, una serif editorial más expresiva, gran presencia del producto y navegación ligera. **Liquid Glass** es un tratamiento selectivo de superficies flotantes, **no** un efecto aplicado a toda la interfaz.

**Usuarios y contexto:**

| Perfil | Contexto | Prioridad de interfaz |
| --- | --- | --- |
| Estudiante COCOA | Busca y reserva desde móvil o computadora, a menudo entre clases | Identificar recursos, consultar fechas y completar una solicitud sin confusión |
| Profesor COCOA | Consulta y solicita recursos para actividades académicas | Acceso claro, reserva rápida y seguimiento del estado |
| Administrador de bodega | Trabaja principalmente con listas, fechas, solicitudes, entregas y devoluciones | Tablas legibles, acciones verificables, alertas y control del inventario |

### Principios

1. **Editorial fuera, preciso dentro:** los grandes titulares se concentran en páginas de entrada y secciones narrativas; formularios, calendarios y panel de administración priorizan claridad.
2. **Una acción principal evidente por contexto:** el botón primario indica el siguiente paso; la solicitud *enviada* no se presenta nunca como *aprobada*.
3. **Producto protagonista:** imágenes reales y consistentes de cámaras, lentes, audio y espacios. No usar fotografías de equipos distintos como si fueran el inventario real.
4. **El estado siempre es explícito:** texto + señal visual; diferenciar el estado de la reserva, el estado físico del equipo y su ocupación temporal.
5. **Glass con propósito:** reservar transparencias y desenfoques para navegación, filtros o paneles elevados, y proporcionar un fallback opaco.
6. **Privacidad visible en el flujo:** un estudiante solo ve su propio historial; las operaciones administrativas se muestran únicamente a roles autorizados. Los permisos se verifican en servidor (PRD §4.5).
7. **Responsive de verdad:** no encoger el diseño de escritorio sin rediseñar jerarquías y controles para móvil.

## 2. Color

La identidad central tiene **cuatro colores**. Los colores de estados son exclusivamente semánticos: no agregan nuevos acentos decorativos a la marca.

| Token | HEX | Nombre | Uso |
| --- | --- | --- | --- |
| `--color-black` | `#000000` | Black | Titulares display, recursos de alto contraste |
| `--color-red` | `#D81C22` | COCOA Red | Acentos editoriales, detalles de marca y CTA ocasionales |
| `--color-coal` | `#1E1E1E` | Coal | Texto principal, botones principales, estado activo |
| `--color-white` | `#FFFFFF` | White | Fondo principal y superficies |
| `--color-paper` | `#F7F6F2` | Paper | Fondos editoriales suaves |
| `--color-soft` | `#F1F0EC` | Soft | Fondo de imágenes y categorías |
| `--color-line` | `#DEDDD8` | Line | Bordes decorativos, separadores |
| `--color-line-strong` | `#C8C7C1` | Line strong | Delimitadores de mayor presencia; verificar contraste en campos |
| `--color-muted` | `#66635D` | Muted | Texto auxiliar y metadatos sobre blanco |

**Peso cromático orientativo del brand board:** 70 % blanco, 15 % negro, 10 % carbón, 5 % rojo. Es una guía de composición, no una métrica obligatoria de píxeles.

### Contraste

- Negro/blanco: **21:1**; carbón/blanco: **aprox. 16.7:1**; rojo/blanco: **aprox. 5.1:1**. Son combinaciones aptas para texto normal.
- **No** usar negro ni carbón como texto sobre rojo; tampoco texto rojo pequeño sobre superficies con transparencia variable.
- El texto sobre vidrio debe conservar **≥ 4.5:1** después de componer la transparencia con lo que hay detrás. Si no se garantiza, usar fondo opaco.
- No usar gris de bajo contraste como texto informativo. El borde decorativo no sustituye el contorno visible de un campo o su foco.

### Colores funcionales

| Estado semántico | Texto | Fondo | Aplicación |
| --- | --- | --- | --- |
| Éxito / aprobado / devuelto | `#23653C` | `#E7F2EA` | Confirmaciones positivas |
| Informativo / en préstamo | `#244C90` | `#E8EEF8` | Estado en curso, información |
| Advertencia / pendiente | `#8A5A00` | `#FFF2D7` | Solicitudes pendientes, precaución |
| Error / rechazo / daño | `#A6282C` | `#FBEAEB` | Errores, rechazado, daño, extravío, atraso |
| Neutro / mantenimiento / cancelación | `#4C4C4C` | `#EFEFEF` | Estados no activos o neutros |

Los estados funcionales deben contrastarse contra su fondo **en el navegador** antes de usarse. Algunos pares podrían necesitar un tono más oscuro en texto si no alcanzan 4.5:1: priorizar accesibilidad por encima del código de color ilustrativo del board. **No reutilizar un color sin texto de estado.**

## 3. Tipografía

La selección viene del moodboard: **Archivo Black** para titulares, **University Roman** para acentos editoriales e **Inter** para lectura e interacción. La v2 del brand board representa el efecto de University Roman mediante **Cormorant Garamond**, fuente de sustitución. University Roman no se debe presentar como implementada hasta contar con el archivo web y la licencia correspondiente.

| Token | Familia / peso | Uso |
| --- | --- | --- |
| `--font-display` | Archivo Black 400 | Titulares y composiciones de alto impacto |
| `--font-editorial` | University Roman, alternativa Cormorant Garamond 400/500, Georgia | Frases editoriales y acentos narrativos |
| `--font-body` | Inter 400/500/600/700/800 | Navegación, datos, fichas, formularios y tablas |

### Escala orientativa

| Uso | Escritorio | Móvil | Estilo |
| --- | ---: | ---: | --- |
| Hero / display | 80–112 px | 48–60 px | Archivo Black; interlineado 0.95 |
| Título principal | 48–62 px | 32–40 px | Archivo Black; interlineado 1.0 |
| Título de sección | 34–48 px | 26–32 px | Archivo Black o serif editorial según contexto |
| Acento editorial | 40–74 px | 28–44 px | University Roman / alternativa |
| Subtítulo funcional | 20–24 px | 18–20 px | Inter 600/700 |
| Texto general | 16 px | 16 px | Inter 400, interlineado 1.5–1.6 |
| Botones | 14–16 px | 14–16 px | Inter 600/700 |
| Metadatos y estados | **14 px mínimo en producto** | **14 px mínimo** | Inter 500/700 |

**Excepción del documento de presentación:** la v2 del brand board usa algunas etiquetas de 11–13 px como recurso de maqueta. **No copiar esos tamaños a pantallas operativas**: fijar mínimo de 14 px para textos informativos, estados, fechas y ayudas. En una próxima iteración del brand board se deben armonizar esas etiquetas con la regla de producción.

No condensar ni estirar horizontalmente Archivo Black para imitar una tipografía condensada. Mantener saltos de línea deliberados, márgenes amplios y texto de lectura izquierda alineado. Evitar más de dos estilos tipográficos protagonistas en el mismo bloque.

## 4. Espaciado, forma y retícula

| Token | Valor | Uso sugerido |
| --- | --- | --- |
| `--space-1` | 4 px | Separaciones mínimas |
| `--space-2` | 8 px | Icono y texto; detalle cercano |
| `--space-3` | 12 px | Elementos compactos |
| `--space-4` | 16 px | Campos, tarjetas y separación estándar |
| `--space-5` | 24 px | Padding de tarjetas y bloques |
| `--space-6` | 32 px | Separación entre grupos |
| `--space-7` | 48 px | Márgenes / secciones |
| `--space-8` | 64 px | Composición editorial |
| `--space-9` | 88 px | Respiro vertical en escritorio |

| Token | Valor | Uso |
| --- | --- | --- |
| `--radius-control` | 10 px | Controles convencionales si no son píldoras |
| `--radius-card` | 16 px | Tarjetas informativas / componentes base |
| `--radius-panel` | 24 px | Paneles amplios y vistas editoriales |
| `--radius-product` | 26 px | Tarjeta / fotografía protagonista del catálogo |
| `--radius-pill` | 999 px | Navegación, chips, botones, filtros y estados |
| `--shadow-panel` | `0 16px 40px rgba(0,0,0,.07)` | Superficies elevadas grandes |
| `--shadow-soft` | `0 10px 28px rgba(0,0,0,.05)` | Elevación discreta |

**Retícula recomendada (propuesta del equipo):** escritorio de 12 columnas; tablet de 8; móvil de 4. Contenedor máximo cercano a 1320 px, con márgenes fluidos y amplios. La portada puede usar asimetría editorial, pero la tabla, el carrito, el calendario y el checkout deben usar retículas predecibles.

**Regla:** no envolver todo en tarjetas, no abusar de sombras, no ocupar espacios en blanco por decoración. Preferir superficies planas con separadores nítidos cuando sea suficiente.

## 5. Tokens CSS listos para `tokens.css`

Crear `client/src/styles/tokens.css` (o ubicación equivalente según el stack) e importarlo una sola vez. **Usar variables, no hexadecimales dispersos en componentes.** Este bloque es el punto de partida del frontend; el HTML v2 contiene los valores visuales de referencia.

```css
:root {
  /* Identidad */
  --color-black: #000000;
  --color-red: #D81C22;
  --color-coal: #1E1E1E;
  --color-white: #FFFFFF;
  --color-paper: #F7F6F2;
  --color-soft: #F1F0EC;
  --color-line: #DEDDD8;
  --color-line-strong: #C8C7C1;
  --color-muted: #66635D;

  /* Semántica: no usar como acentos decorativos */
  --color-success: #23653C;
  --color-success-bg: #E7F2EA;
  --color-info: #244C90;
  --color-info-bg: #E8EEF8;
  --color-warning: #8A5A00;
  --color-warning-bg: #FFF2D7;
  --color-error: #A6282C;
  --color-error-bg: #FBEAEB;
  --color-neutral: #4C4C4C;
  --color-neutral-bg: #EFEFEF;

  /* Tipografía. University Roman solo si está licenciada. */
  --font-display: "Archivo Black", Impact, sans-serif;
  --font-editorial: "University Roman", "Cormorant Garamond", Georgia, serif;
  --font-body: "Inter", Arial, sans-serif;

  /* Espaciado */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 24px;
  --space-6: 32px;
  --space-7: 48px;
  --space-8: 64px;
  --space-9: 88px;

  /* Forma y elevación */
  --radius-control: 10px;
  --radius-card: 16px;
  --radius-panel: 24px;
  --radius-product: 26px;
  --radius-pill: 999px;
  --shadow-panel: 0 16px 40px rgba(0, 0, 0, .07);
  --shadow-soft: 0 10px 28px rgba(0, 0, 0, .05);

  /* Liquid Glass selectivo */
  --glass-surface: rgba(255, 255, 255, .68);
  --glass-border: rgba(255, 255, 255, .92);
  --glass-blur: 18px;
  --glass-shadow: 0 10px 34px rgba(0, 0, 0, .08);

  /* Interacción */
  --focus-ring: #244C90;
  --control-min-height: 44px;
  --motion-fast: 180ms;
  --motion-standard: 240ms;
}
```

### Patrón Liquid Glass

```css
.glass-surface {
  background: var(--glass-surface);
  border: 1px solid var(--glass-border);
  border-radius: var(--radius-pill);
  box-shadow: var(--glass-shadow);
  -webkit-backdrop-filter: blur(var(--glass-blur)) saturate(130%);
  backdrop-filter: blur(var(--glass-blur)) saturate(130%);
}

@supports not ((backdrop-filter: blur(1px)) or
               (-webkit-backdrop-filter: blur(1px))) {
  .glass-surface {
    background: var(--color-white);
    border-color: var(--color-line);
  }
}

@media (prefers-reduced-transparency: reduce) {
  .glass-surface {
    background: var(--color-white);
    -webkit-backdrop-filter: none;
    backdrop-filter: none;
  }
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    scroll-behavior: auto !important;
    transition-duration: .01ms !important;
    animation-duration: .01ms !important;
  }
}
```

No usar glass encima de fondos que cambien la legibilidad del texto ni en tablas extensas. La transparencia **no** justifica ocultar los bordes ni los estados de foco. No multiplicar zonas de blur por toda la página, especialmente en móvil.

## 6. Componentes y reglas de interacción

| Componente | Forma y tipografía | Contenido / comportamiento obligatorio |
| --- | --- | --- |
| **Navbar** | Horizontal, limpia; versión flotante glass en páginas públicas/interiores cuando no obstaculice | Logo, catálogo, espacios, mis reservas, perfil; enlaces claros; en móvil priorizar acciones principales |
| **Navegación móvil** | Cápsula flotante o barra inferior compacta | Etiquetas comprensibles e iconos; estado activo; no superponer al botón de checkout ni contenido importante |
| **Botón primario** | Coal `#1E1E1E` con texto blanco, radio píldora, alto ≥44 px | Una acción principal; nombre accionable («Enviar solicitud»), nunca «Reserva confirmada» antes de aprobación |
| **Botón secundario** | Blanco, borde carbón, texto carbón | Acciones auxiliares o retorno |
| **Botón acento** | Rojo `#D81C22`, texto blanco | Uso selectivo en CTA editorial; no competir con un primario cercano |
| **Campo / formulario** | Inter 16 px, etiqueta persistente, borde visible | Ayuda breve, errores debajo del campo, validación sin borrar los datos ingresados |
| **Buscador** | Píldora con icono y placeholder específico | Buscar por nombre / categoría / tipo; permitir vaciar y recuperar resultados |
| **Filtros y calendario** | Chips de estado y celdas de fechas legibles | Mostrar seleccionado, no disponible y habilitado con texto y diferencia visual; horario 24 h y bloques previstos de 30 min |
| **Tarjeta de equipo** | Superficie clara; imagen amplia, radio de producto, Inter | Foto verificable, nombre, tipo, datos pertinentes, disponibilidad para fechas elegidas y acción «Ver equipo» |
| **Tarjeta de espacio** | Fotografía que muestre el espacio real | Nombre, capacidad/detalles configurados, fechas disponibles y si se reserva completo o por estación |
| **Detalle de recurso** | Retícula imagen/información, móvil apilado | Hasta tres imágenes, descripción y datos del PRD, selector de fechas, CTA para añadir al carrito |
| **Carrito** | Lista clara de ítems y resumen separado | Fechas, cantidades, recursos y vencimiento de 1 h; posibilidad de retirar artículos; mensaje antes de perder contenido |
| **Checkout** | Formulario de baja fricción | Resumen, motivo académico, aceptación de políticas, «Enviar solicitud»; confirmar explícitamente «Pendiente de aprobación» |
| **Mis reservas** | Lista/tarjetas por fecha + estados | Próximas, anteriores, comprobante e información de retiro, cancelación cuando proceda |
| **Dashboard** | Sobrio, sin hero publicitario | Pendientes, retiros, devoluciones e incidencias; filtros; acciones administrativas con confirmación |
| **Tabla administrativa** | Filas legibles y acciones claras | Orden por prioridad operativa; columnas adaptadas a móvil sin ocultar datos críticos |
| **Checklist de entrega** | Lista por unidad, con casillas y resumen | Cada ítem efectivamente entregado, responsable, momento; permitir registrar faltantes y discrepancias según PRD |
| **Checklist de devolución** | Lista y estado por unidad | Entregado/devuelto, daños, faltantes y registro del administrador; no declarar libre un artículo sin verificación |
| **Modal / drawer** | Preferir superficie opaca; glass solo en borde/panel no crítico | Título, contexto, botones inequívocos, cierre por teclado, foco contenido y restaurado |
| **Toast / aviso** | Superficie con texto e icono | Informar resultado y siguiente acción; no ser único canal de errores críticos |

### Estados del componente (obligatorios)

| Estado UI | Ejemplo de texto | Comportamiento |
| --- | --- | --- |
| Cargando | «Consultando disponibilidad…» | Mostrar progreso legible; no disparar la misma operación repetidamente |
| Vacío | «Todavía no tienes reservas próximas.» | Mostrar siguiente acción: «Explorar catálogo» |
| Error recuperable | «No pudimos cargar los horarios. Inténtalo de nuevo.» | Explicar la situación y ofrecer reintento |
| Error de validación | «Selecciona una fecha de devolución válida.» | Mostrar junto al campo pertinente, con foco accesible |
| Éxito de solicitud | «Solicitud enviada. Está pendiente de aprobación.» | Mostrar comprobante/identificador y enlace a Mis reservas |
| Éxito administrativo | «Reserva aprobada. Se notificará al solicitante.» | Actualizar estado y auditoría; no afirmar envío de correo antes de confirmarlo |
| Sin disponibilidad | «Este equipo no está disponible para esas fechas.» | Ofrecer otra fecha o recurso, sin mentir sobre unidades |

### Cambios de estado de una reserva

No crear estados nuevos porque hagan falta colores bonitos. Según PRD §4.4, los rótulos son:

| Estado de reserva | Rótulo en pantalla | Tratamiento semántico |
| --- | --- | --- |
| `pendiente` | **Pendiente de aprobación** | Advertencia |
| `aprobada` | **Aprobada** | Éxito |
| `en_prestamo` | **En préstamo** | Información |
| `devuelta` | **Devuelta** | Éxito |
| `rechazada` | **Rechazada** | Error |
| `cancelada` | **Cancelada** | Neutro |
| Indicador calculado | **Devolución atrasada** | Error / alerta, sin convertirlo automáticamente en un estado terminal |

Flujo principal: `pendiente → aprobada → en_prestamo → devuelta`. `rechazada` y `cancelada` interrumpen el flujo. **Las transiciones exactas son propuesta del PRD y aún requieren validación**; no permitir acciones irreversibles desde la interfaz sin comprobar permisos y reglas.

### Estados de inventario y disponibilidad

La existencia de una reserva **no cambia automáticamente la condición física** de una unidad. Representar la condición y la ocupación por fecha como dimensiones separadas.

| Contexto | Rótulo | Cómo mostrarlo |
| --- | --- | --- |
| Disponible para las fechas elegidas | **Disponible** | Positivo; con fechas si corresponde |
| No elegible o ocupado en las fechas | **No disponible** | Neutro con explicación breve |
| Ocupado por reserva aprobada | **Reservado** | Advertencia; indicar período |
| Ya retirado | **En préstamo** | Informativo; seguimiento administrativo |
| Condición física | **En mantenimiento** | Neutro, no elegible |
| Condición física | **Dañado** | Error, no elegible |
| Condición física | **Extraviado** | Error, no elegible |

La vista del estudiante puede resumir la disponibilidad sin revelar información de otros usuarios. El administrador puede consultar el estado y las incidencias. **Los nombres exactos del modelo persistido se decidirán en el avance 3; no confundirlos con etiquetas de UI.**

## 7. Datos y microcopy

| Dato | Formato en pantalla | Ejemplo |
| --- | --- | --- |
| Fecha corta | Día de la semana + día + mes, en español | `mar 24 nov` |
| Fecha completa | Día, mes y año | `24 de noviembre de 2026` |
| Hora | 24 horas, zona Ecuador | `08:30`, `16:30` |
| Rango | Inicio–fin, con separador claro | `08:30–10:00` |
| Retiro y devolución | Etiquetas distintas | `Retiro: mar 24 nov · 10:00` / `Devolución: jue 26 nov · 16:30` |
| Unidades | Número + sustantivo | `2 unidades disponibles` |
| Recurso individual | Nombre + código si existe | `Cámara Sony FX3 · Unidad 02` |
| Reserva | Identificador consistente | `#BC-1042` (ilustrativo) |
| Carrito | Tiempo visible cuando corresponda | `Tu carrito vence en 12 min` |
| Recordatorios | Indicar el evento exacto | `Retira tu equipo a las 10:00` / `Devuelve tu equipo a las 16:30` |

**Horarios importantes del PRD:** el cliente anotó atención entre **08:30 y 17:20** y franjas de **30 minutos**. **No** mostrar un último turno ficticio mientras no se confirme cómo se resuelve la incompatibilidad entre ambos valores. Las reservas requieren aprobación humana. Los correos de recordatorio están previstos para **30 min antes de retirar** y **30 min antes de devolver**, solo si la reserva sigue aprobada/vigente.

**Datos simulados:** todos los ejemplos de producto, stock, precio, foto y número de reserva del brand board son ilustrativos. No convertirlos en datos del catálogo real. Como es un préstamo, **no mostrar precios de venta ni botones «Comprar»**.

## 8. Tono de voz

Español claro, directo y humano; tuteo consistente; frases cortas y útiles. La identidad puede incorporar frases editoriales en inglés en espacios de marca, pero las acciones de reserva, los errores y las políticas se entienden sin saber inglés.

| Así sí | Así no |
| --- | --- |
| «Tu solicitud está pendiente. COCOA la revisará y te avisará por correo.» | «¡Reserva confirmada!» antes de aprobación |
| «Este equipo no está disponible para esas fechas. Prueba con otro horario.» | «Error 409: stock conflict» |
| «Tu reserva fue aprobada. Revisa la hora de retiro.» | «Su requerimiento ha sido procesado exitosamente.» |
| «Devuelve tus equipos a las 16:30. Te enviaremos un aviso 30 minutos antes.» | «Tienes que venir a dejar tus cosas ASAP.» |
| «Falta verificar 1 equipo de tu checklist.» | «No se puede finalizar.» |

**No:** tecnicismos para usuarios, metáforas que oculten acciones, tono infantil, humor en errores, mensajes que confundan *solicitud* con *reserva aprobada*.

## 9. Accesibilidad, responsive y rendimiento

- Textos informativos en producto con **contraste ≥ 4.5:1**; verificar sobre el fondo efectivo, especialmente con Liquid Glass.
- Objetivos táctiles de al menos **44 × 44 px**, con excepciones justificadas y espacio suficiente.
- Campos con `<label>` real; iconos de solo imagen con nombre accesible. No usar placeholder como sustituto de etiqueta.
- Estados con texto + forma/icono; nunca solo color.
- Foco visible; elementos semánticos reales (`button`, `a`, `input`, `table`); orden de tabulación coherente.
- Menús, diálogos, selector de fechas y tabs accesibles por teclado y lectores de pantalla.
- Respetar `prefers-reduced-motion` y ofrecer alternativa opaca cuando la transparencia afecte la lectura.
- En móvil, prioridad al buscador, categorías, fechas, carrito y reservas; la barra flotante no puede bloquear contenido o teclado.
- Imágenes del catálogo con `alt` descriptivo, carga diferida cuando no sean críticas y dimensiones estables para evitar saltos.
- Limitar desenfoques grandes, efectos simultáneos y animaciones decorativas. La interacción debe seguir siendo rápida en equipos modestos.
- En contexto administrativo, nunca ocultar acciones críticas solo por `hover`.

## 10. No hacemos

1. No copiamos literalmente Arts Gallery, Books ni Zerouge: son referencias de ritmo, composición y tratamiento visual.
2. No usamos gradientes tecnológicos morados/azules, neones, emojis como iconos, sombras pesadas ni paneles glass en toda la página.
3. No usamos Archivo Black para párrafos, fichas técnicas, tablas ni formularios.
4. No sacrificamos legibilidad para hacer el diseño “más editorial”.
5. No mostramos una solicitud pendiente como confirmada.
6. No presentamos datos ficticios como inventario real ni fotografías que no corresponden al recurso.
7. No implementamos pagos, calificación algorítmica, multas automáticas o renovaciones sin respaldo en el PRD.
8. No inferimos roles o permisos solo desde botones escondidos: la seguridad se aplica en backend y base de datos.
9. No añadimos pantallas o estados no previstos sin actualizar el PRD, el brand board y este archivo.
10. No usamos la fuente University Roman sin licencia web válida.

## 11. Control de coherencia antes de implementar

- [ ] El PRD, el brand board y `DESIGN.md` usan los mismos términos para solicitudes y estados.
- [ ] Ninguna maqueta afirma que una solicitud se aprueba automáticamente.
- [ ] La disponibilidad depende de fechas y de condición operativa, no solo de una etiqueta estática.
- [ ] Todo texto de estado conserva contraste y tamaño apropiados en producción.
- [ ] La fuente editorial implementada corresponde a una licencia válida; hasta entonces se usa la alternativa identificada.
- [ ] El tratamiento Liquid Glass sigue siendo selectivo y tiene fallback opaco.
- [ ] Se conserva el checklist administrativo de entrega y devolución.
- [ ] Los dos recordatorios de 30 min están diferenciados por evento.
- [ ] Los ejemplos del brand board permanecen marcados como ilustrativos.
- [ ] Los supuestos del PRD no se implementan como hechos confirmados sin decisión del equipo.

---

**Uso y mantenimiento:** este archivo vive en la raíz del repositorio como contrato visual para el equipo y el agente de desarrollo. Los tokens pertenecen a `tokens.css`, los componentes respetan sus reglas y toda modificación visible debe mantenerse sincronizada con `docs/diseno/brand-board.html`.
