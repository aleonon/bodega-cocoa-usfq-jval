# PRD — Bodega COCOA

> **Proyecto final · Desarrollo Web 3 · Universidad San Francisco de Quito**  
> **Versión:** 1.0 · 22 de noviembre de 2026  
> **Equipo:** Juanes Vargas y Ailyn León  
> **Cliente:** Bodega COCOA, USFQ  
> **Estado:** documento base para validación y desarrollo del MVP  
> **Fuentes:** brief del equipo del 11 de noviembre de 2026; notas de la visita del cliente incluidas en las páginas 3–5 de `Entrevista.pdf`; aclaraciones posteriores del equipo del 22 de noviembre de 2026. El material visual de `MOODBOARD WEB 3.pdf` guía el brand board y `DESIGN.md`, no las reglas del negocio.

## 1. Problema y objetivo

La plataforma de reservas utilizada actualmente por Bodega COCOA dificulta encontrar equipos y espacios, reservar varios artículos en una sola solicitud, comprender los horarios disponibles, acceder a las cuentas y conocer el estado de una reserva. La navegación y la presentación del catálogo resultan poco intuitivas. Esto genera confusión para los estudiantes y más trabajo manual para quienes administran los préstamos. El registro de entregas, devoluciones y cambios de estado también necesita mayor trazabilidad.

**Objetivo:** construir una plataforma web adaptable a computadoras y móviles que permita a las personas autorizadas de COCOA explorar un catálogo de equipos audiovisuales y espacios, solicitar varios artículos mediante un carrito y seguir sus reservas; y que permita al personal de la bodega aprobar solicitudes manualmente, controlar la disponibilidad y el estado de cada unidad, registrar las entregas y devoluciones y consultar reportes desde un solo lugar.

**Principio de producto:** *Less friction. More creation.* Menos pasos confusos para quienes reservan; más control y trazabilidad para quienes administran.

## 2. Usuarios

| Perfil | Quién es | Qué necesita hacer | Restricción principal |
| --- | --- | --- | --- |
| Estudiante COCOA | Estudiante autorizado de COCOA, con cuenta institucional | Iniciar sesión, explorar el catálogo, consultar disponibilidad, crear y cancelar solicitudes, consultar su historial, recibir avisos y presentar su reserva al retirar equipos | Solo ve sus propios datos y reservas; solo puede solicitar si su cuenta está habilitada |
| Profesor COCOA | Docente autorizado para utilizar recursos de COCOA | Reservar equipos o espacios para actividades académicas y consultar sus solicitudes | Acceso institucional y habilitación administrativa; reglas específicas por confirmar |
| Administrador de bodega | Personal autorizado de COCOA responsable de préstamos e inventario | Habilitar cuentas, revisar y aprobar o rechazar reservas, ajustar solicitudes, controlar equipos y espacios, verificar entregas y devoluciones, gestionar restricciones y obtener reportes | Acceso exclusivo a operaciones administrativas; toda acción sensible queda registrada |

Una autenticación correcta con Microsoft **no equivale** a una autorización para reservar. Las cuentas deben estar aprobadas por la administración de COCOA.

## 3. Alcance del MVP

Las siguientes funcionalidades constituyen la propuesta de MVP para el avance funcional y la presentación final. Las características señaladas como supuestos en §7 deberán validarse antes de su implementación definitiva.

1. **Acceso institucional:** permitir inicio y cierre de sesión mediante Microsoft institucional, con comprobación de una cuenta habilitada por COCOA.
2. **Gestión de cuentas:** permitir al administrador registrar o habilitar usuarios autorizados, asignarles un rol, deshabilitarlos y establecer bloqueos temporales.
3. **Catálogo:** mostrar equipos, accesorios, kits y espacios existentes, organizados por categorías, con búsqueda y filtros.
4. **Fichas de recursos:** mostrar de uno a tres imágenes por artículo, descripción, características, identificador cuando corresponda, disponibilidad y condiciones relevantes.
5. **Calendario de disponibilidad:** consultar días y franjas horarias disponibles antes de agregar un recurso a una solicitud, diferenciando equipos de espacios.
6. **Carrito único por proceso:** agregar varios artículos y/o espacios a una solicitud, revisar cantidades y fechas y conservar el carrito activo hasta una hora.
7. **Checkout de reserva:** solicitar el propósito del préstamo, presentar las políticas y términos y permitir enviar una solicitud de aprobación manual.
8. **Aprobación administrativa:** notificar por correo al administrador sobre una solicitud nueva y permitirle aprobarla o rechazarla desde el panel web.
9. **Comunicación del resultado:** informar al solicitante el resultado de la revisión y mostrar el estado de la solicitud en su cuenta; no presentar una solicitud pendiente como aprobada.
10. **Mis reservas:** mostrar próximas solicitudes, estados, detalles, comprobantes e historial para facilitar el retiro.
11. **Cancelación:** permitir al solicitante cancelar desde la web hasta una hora antes del inicio previsto, cuando la reserva reúna las condiciones para cancelación.
12. **Recordatorios por correo:** programar un mensaje al correo registrado 30 minutos antes del inicio del préstamo y otro 30 minutos antes de la devolución prevista, solo para reservas aprobadas y vigentes.
13. **Panel administrativo:** listar y filtrar solicitudes por estado, fecha, usuario y horario; mostrar las tareas que requieren atención.
14. **Gestión de inventario:** permitir al administrador crear, editar, deshabilitar o retirar del catálogo recursos, actualizar imágenes y gestionar unidades identificadas, kits y estados del equipo.
15. **Control de disponibilidad:** impedir confirmar solicitudes incompatibles con el inventario, los bloqueos, el mantenimiento y los horarios permitidos.
16. **Entrega verificada:** proporcionar al administrador un checklist por artículo/unidad para confirmar qué se entregó efectivamente y registrar fecha, hora y responsable.
17. **Devolución registrada:** permitir al administrador comprobar la devolución de artículos, registrar faltantes o daños y actualizar su disponibilidad.
18. **Espacios y estaciones:** permitir consultar y solicitar un espacio completo o estaciones individuales cuando estas estén configuradas como recursos separados.
19. **Reportes y comprobantes:** ofrecer un comprobante por reserva y exportación de datos de reservas en Excel y PDF para la administración.
20. **Trazabilidad y privacidad:** guardar cambios de estado y acciones administrativas relevantes, proteger las rutas por rol y limitar la exposición de datos personales.

**Criterio de alcance:** los requisitos anteriores son la referencia funcional del MVP; cualquier integración o automatización no confirmada se documenta en §7 o §5, no se asume como aprobada.

## 4. Reglas de negocio

### 4.1 Acceso, usuarios y permisos

1. Solo pueden solicitar recursos las cuentas de estudiantes y profesores de COCOA que hayan sido habilitadas por un administrador.
2. El inicio de sesión se hará con Microsoft institucional. La integración propuesta es Supabase Auth con el proveedor Microsoft; la elección tecnológica final deberá verificarse técnicamente.
3. El administrador controla las altas, habilitaciones, restricciones y deshabilitaciones de cuentas. No habrá registro público con acceso automático al catálogo reservable.
4. Cada usuario solo podrá consultar y modificar sus propias solicitudes mediante las acciones que se le permitan; únicamente los administradores accederán a datos globales e inventario editable.
5. Los bloqueos de usuarios tendrán una fecha o duración establecida por el administrador. Mientras esté vigente el bloqueo no podrán generarse nuevas solicitudes. La política exacta de multas sigue abierta (§7).

### 4.2 Catálogo e inventario

6. Solo se podrán solicitar recursos elegibles y disponibles para el período seleccionado. Un equipo dañado, extraviado o en mantenimiento no puede incluirse en una nueva reserva aprobada.
7. El sistema debe permitir que un mismo modelo tenga unidades individuales identificables cuando COCOA requiera trazabilidad por número o código, y también manejar artículos sin identificación individual.
8. El administrador podrá añadir, editar y retirar artículos de catálogo, registrar entre **una y tres imágenes** y modificar sus estados y notas internas.
9. Se distinguen dos conceptos: **estado físico/operativo del recurso** y **estado de su ocupación por reservas**. Una cámara operativamente apta puede estar reservada en una fecha determinada; «reservado» no significa que esté dañada ni elimina su disponibilidad para otros períodos.
10. Los equipos tendrán al menos la información necesaria para mostrar al estudiante «Disponible», «No disponible» o «En mantenimiento» según el contexto. La vista administrativa distinguirá también «Dañado» y «Extraviado». La correspondencia exacta entre los cinco rótulos de las notas del cliente y el modelo interno se detalla como supuesto en §7.
11. Un espacio completo y cada estación individual son recursos distintos cuando el administrador así los configure. **La regla de exclusividad entre reservar el espacio completo y reservar sus estaciones debe validarse** (§7).

### 4.3 Reserva y disponibilidad

12. Un carrito agrupa varios recursos en **una sola solicitud**. Tras enviarla, el carrito se vacía; el usuario puede iniciar otra solicitud para fechas diferentes. No hay un límite general confirmado de reservas por estudiante.
13. El carrito puede permanecer abierto **como máximo una hora** desde su inicio. Al vencer, se descarta su contenido no enviado; se informará al usuario antes de perderlo (comportamiento exacto del aviso: supuesto).
14. La interfaz utilizará formato de **24 horas** y selección de horarios en intervalos de **30 minutos**.
15. Los retiros solo pueden programarse dentro del horario operativo indicado por el cliente: **08:30–17:20**, hora de Ecuador, en días hábiles habilitados. Como 17:20 no coincide con la cuadrícula de 30 minutos, el último turno válido queda pendiente de confirmación (§7).
16. No se permitirá programar retiros fuera del horario de atención ni en feriados o días bloqueados. Las restricciones de devolución y el horario de espacios deben confirmarse por separado (§7).
17. El cliente mencionó una **separación de 30 minutos entre reservas**. Se implementará solo cuando se confirme si corresponde a colchón entre préstamos, turnos de retiro, uso de espacios u otra operación (§7); no se asumirá que afecta a todos los recursos de la misma forma.
18. La solicitud puede hacerse sin una antelación mínima adicional a las reglas de horario y disponibilidad; su efectividad depende de aprobación administrativa antes del retiro. La consecuencia de solicitudes inmediatas sin tiempo suficiente para aprobar está abierta (§7).
19. La duración del préstamo dependerá del motivo académico y puede llegar hasta **un semestre**, sujeto a revisión administrativa. No existe renovación automática del préstamo.
20. Cada solicitud debe incluir un comentario sobre su finalidad, por ejemplo tesis, documental, clase o proyecto.
21. El envío de la solicitud **no equivale a aprobación**. Su estado inicial es «Pendiente de aprobación» y debe ser revisada manualmente por un administrador.
22. Al crearse una solicitud pendiente, se envía un correo al administrador; al aprobarla o rechazarla, el usuario recibe una notificación al correo de su cuenta.
23. Antes de aprobar, el sistema vuelve a comprobar disponibilidad y conflictos para evitar que se aprueben dos reservas incompatibles.
24. La autorización parcial de artículos de una misma solicitud, el efecto de solicitudes pendientes sobre disponibilidad y la prioridad exacta «por orden» no están confirmados (§7).
25. El administrador puede intervenir o modificar el contenido de una solicitud; el alcance de esa potestad y cómo se informa al usuario se documentan como preguntas abiertas (§7).
26. El usuario podrá cancelar una reserva desde la plataforma **hasta una hora antes** del inicio previsto; las excepciones y las cancelaciones administrativas quedan sujetas a validación.
27. Los recordatorios automáticos se envían **30 minutos antes del inicio previsto** y **30 minutos antes de la devolución prevista**, exclusivamente a la dirección asociada a la cuenta autorizada. Una reserva cancelada o rechazada no recibirá recordatorios de retiro/devolución.

### 4.4 Entrega, devolución y seguimiento

28. El administrador registra la entrega real a través de un checklist de los artículos y unidades incluidas en la reserva; la lista deberá reflejar los ítems efectivamente entregados, incluso ante una entrega incompleta.
29. El administrador registra la devolución real mediante verificación de los artículos y su condición. Hasta que se registre o se resuelva una incidencia, el equipo no se vuelve a ofrecer automáticamente como disponible por el solo transcurso del horario programado (**supuesto operativo**).
30. Un equipo registrado como dañado, extraviado o en mantenimiento queda excluido de nuevas aprobaciones mientras conserve ese estado.
31. El administrador puede consultar el historial de reservas, entregas y devoluciones y registrar incidencias relevantes. Las multas y un puntaje de estrellas requerirán reglas adicionales antes de automatizarse (§5 y §7).
32. Los estados propuestos para el ciclo de la solicitud son: **Pendiente de aprobación → Aprobada → En préstamo → Devuelta**. También pueden terminar como **Rechazada** o **Cancelada**; **Vencida / con devolución atrasada** es un indicador que depende de fecha y devolución efectiva. La formalización de transiciones se validará con el cliente.

### 4.5 Privacidad y seguridad

33. Las operaciones administrativas se autorizan en el servidor y la base de datos, no solo ocultando botones en la interfaz.
34. La base de datos guarda únicamente los datos personales necesarios para identificar al usuario, autorizar el préstamo y conservar su historial operativo. No se almacenarán contraseñas de Microsoft.
35. Los registros administrativos sensibles deben identificar quién realizó cada acción y cuándo, con acceso limitado al personal autorizado.
36. Los comprobantes, exports y correos no expondrán datos personales de otros estudiantes. Se utilizarán conexiones cifradas y secretos fuera del código fuente.

## 5. Fuera de alcance del MVP

| Funcionalidad o idea mencionada | Decisión para esta entrega | Motivo |
| --- | --- | --- |
| Chatbot o bot de WhatsApp | Fuera del MVP | En las notas se considera deseable, pero no indispensable; añade integraciones y mantenimiento |
| Aplicación móvil nativa | Fuera del MVP | La web adaptable cubre escritorio y móvil sin dos aplicaciones separadas |
| Renovación automática de préstamos | Fuera del MVP | El cliente indicó que no aplica un sistema de renovación |
| Cálculo y cobro automatizado de multas | Fuera del MVP, salvo reglas posteriormente confirmadas | No hay tabla de sanciones, montos, criterios de aplicación ni proceso de apelación definidos |
| Calificación automática de usuarios con estrellas | Fuera del MVP | Se mencionó un score, pero no se definieron criterios verificables ni consecuencias; evitar valoraciones arbitrarias |
| Sincronización con plataformas externas de inventario | Fuera del MVP | No hay formato, permisos ni conexión definidos; el catálogo se podrá gestionar manualmente |
| Funciones de inteligencia artificial para aprobar reservas | Fuera del MVP | La aprobación solicitada es humana y explícita |

El **registro de bloqueos y de incidencias** sí pertenece al MVP; lo que se pospone es el cálculo automático de multas o reputación.

## 6. Decisiones del cliente y aclaraciones posteriores

> **Jerarquía de evidencia:** las notas directas de la visita prevalecen sobre los resúmenes automáticos; las aclaraciones posteriores del equipo prevalecen para el diseño del proyecto, aunque conviene ratificarlas con el cliente si implican una regla nueva. Esta tabla distingue ambas fuentes.

| ID | Fecha | Fuente | Decisión o información | Implicación |
| --- | --- | --- | --- | --- |
| D01 | 11 nov 2026 | Visita del cliente, notas p. 3 | Primera entrega funcional el 2 de diciembre | Priorizar un MVP demostrable |
| D02 | 11 nov 2026 | Visita, pp. 3–4 | Reservas agrupadas en un carrito; no renovación automática; no límite general de solicitudes | Carrito único por proceso y reservas independientes |
| D03 | 11 nov 2026 | Visita, pp. 3–5 | Uso de bloques de 30 minutos y horario de atención 08:30–17:20; no retirar en horarios no laborales o feriados | Validaciones temporales y calendario |
| D04 | 11 nov 2026 | Visita, p. 4 | Inicio con Microsoft institucional mediante opción Supabase; administrador gestiona cuentas | Autenticación federada + habilitación por rol |
| D05 | 11 nov 2026 | Visita, pp. 3–4 | El carrito dura una hora y se vacía tras enviar; requiere justificar finalidad del préstamo | Temporizador y campo de propósito |
| D06 | 11 nov 2026 | Visita, p. 4 | Préstamos según motivo, hasta un semestre; cancelación una hora antes | Duración revisada y plazo de cancelación |
| D07 | 11 nov 2026 | Visita, pp. 4–5 | Administrador edita catálogo, distingue estados, puede configurar imágenes, kits y unidades | Herramientas de inventario y estados visibles |
| D08 | 11 nov 2026 | Visita, p. 4 | Posibilidad de reservar espacios completos o estaciones individuales | Tipos y relaciones de recursos |
| D09 | 11 nov 2026 | Visita, pp. 3–5 | Checklist para pedidos extensos; reportes en Excel/PDF; historial y comprobantes | Control de entrega, exportación e historial |
| D10 | 11 nov 2026 | Visita, p. 5 | Términos y condiciones, calendario legible y estética COCOA/USFQ | Checkout claro y guía de diseño |
| D11 | 11 nov 2026 | Visita, pp. 4–5 | Bloqueos temporales, posible score y multas; chatbot opcional | Bloqueos básicos en MVP; automatizaciones complejas pendientes |
| A01 | 22 nov 2026 | Aclaración del equipo | Se construirán frontend de usuario, panel administrativo, backend y base de datos | Alcance técnico integral |
| A02 | 22 nov 2026 | Aclaración del equipo | Toda reserva requiere aprobación manual; llega correo al administrador | Flujo pendiente → revisión → decisión |
| A03 | 22 nov 2026 | Aclaración del equipo | Varias reservas en diferentes fechas sí son posibles; carrito agrupa recursos de una solicitud | No imponer límite de una reserva total |
| A04 | 22 nov 2026 | Aclaración del equipo | Solo usuarios COCOA; Microsoft no elimina el filtro de autorización del administrador | Control de acceso por organización y estado |
| A05 | 22 nov 2026 | Aclaración del equipo | Checklist administrativo al entregar equipos | Verificación y trazabilidad de salida |
| A06 | 22 nov 2026 | Aclaración del equipo | Correo al usuario 30 minutos antes del retiro y 30 minutos antes de devolver | Sistema de recordatorios programados |
| A07 | 22 nov 2026 | Aclaración del equipo | El administrador mantiene control de los estados del inventario | Gestión operativa permanente |
| A08 | 22 nov 2026 | Aclaración del equipo | No hay stack obligatorio; privacidad, flexibilidad y protección de cuentas son prioritarias | Elección técnica documentada y medidas de seguridad |

**Contradicciones del primer avance aún relevantes:** los resúmenes discrepan sobre costo mensual (USD 150 frente a USD 1,50), naturaleza de la entrega de diciembre y algunos horarios. Ninguno de estos valores contradictorios se usará como decisión de arquitectura o presupuesto sin confirmación.

## 7. Supuestos y preguntas abiertas

Cada supuesto es provisional. No sustituye una respuesta del cliente.

| ID | Prioridad | Pregunta pendiente | Supuesto de trabajo hasta confirmación |
| --- | --- | --- | --- |
| S01 | Alta | ¿Una solicitud pendiente aparta inventario y durante cuánto tiempo? | La solicitud pendiente **no consume definitivamente** inventario; la disponibilidad se revalida al aprobar |
| S02 | Alta | ¿El administrador puede aprobar solo una parte del carrito o debe decidir sobre toda la solicitud? | Aprobar o rechazar la solicitud completa; si falta algo, solicitar nueva selección antes de aprobar |
| S03 | Alta | ¿Qué ocurre con reservas aprobadas si un equipo pasa a mantenimiento o se daña? | Marcar conflicto y alertar al administrador; no reasignar ni cancelar automáticamente |
| S04 | Alta | ¿Qué significa «por orden» al revisar reservas simultáneas? | Ordenar la cola por hora de envío, pero la aprobación sigue siendo manual |
| S05 | Alta | ¿Cuál es el último turno permitido con horario 08:30–17:20 y bloques de 30 min? | Mostrar franjas desde 08:30 y no aceptar retiros posteriores a 17:20; el último turno específico requiere validación |
| S06 | Alta | ¿Los 30 minutos «entre reservas» son separación de uso, intervalos del calendario o turnos de atención? | Solo discretización del selector en 30 min hasta aclararlo; no bloquear 30 min extra entre préstamos |
| S07 | Alta | ¿Cuándo se libera un equipo no retirado y cómo se determina una devolución atrasada? | Solo el administrador libera o cierra una solicitud no retirada; la devolución atrasada se identifica sin liberar inventario automáticamente |
| S08 | Alta | ¿Qué pasa cuando se solicita para empezar en menos de 30 minutos y aún no hay aprobación? | El usuario puede solicitar dentro de horario; no se entrega ni se envía recordatorio hasta la aprobación; advertir que la solicitud puede no atenderse a tiempo |
| S09 | Alta | ¿Cómo se relaciona la reserva del estudio completo con la de estaciones individuales? | El espacio completo bloquea sus estaciones y viceversa en el período compartido |
| S10 | Media | ¿Todas las reservas de profes siguen las mismas reglas y requieren su propio usuario? | Profes autorizados utilizan el mismo flujo de solicitud que estudiantes |
| S11 | Media | ¿Qué puede modificar el administrador de un carrito ya enviado y cuándo se pide aceptación del usuario? | Puede proponer ajustes antes de aprobar; se registra el cambio y se comunica al usuario |
| S12 | Media | ¿Qué artículos llevan unidad identificada y aplica la referencia de USD 500? | La trazabilidad por unidad será configurable por artículo; no se impondrá el umbral económico hasta ratificación |
| S13 | Media | ¿Los kits descuentan automáticamente sus piezas y cómo se representan accesorios sin ID? | Kits como agrupaciones de recursos; unidades de cada componente se validan al aprobar |
| S14 | Media | ¿Qué evidencia o firma se requiere para la entrega y la devolución? | Checklist con responsable, marcas de cada artículo y marca de tiempo; sin firma digital obligatoria |
| S15 | Media | ¿Qué información exacta llevará el comprobante y qué significa «cada reserva genera Excel»? | Comprobante descargable/consultable por reserva; exportación Excel/PDF disponible desde administración |
| S16 | Media | ¿Quién recibe el aviso al administrador: uno o varios correos? ¿Se espera confirmación de entrega? | Destinatarios configurables; registro de intentos y reintentos, sin asumir que correo enviado equivale a leído |
| S17 | Media | ¿Se notifican también los cambios de fecha, cancelaciones y rechazos? | Avisar resultado de aprobación y cancelaciones; reprogramar recordatorios cuando haya cambios confirmados |
| S18 | Media | ¿Se permite cancelar exactamente a 60 minutos del inicio? | Sí, hasta inclusive el límite de 60 min; después solo administración podrá resolverlo |
| S19 | Media | ¿Cuál es el proceso y escala de multas, bloqueo y score? | Guardar historial de incidencias y bloqueos manuales; sin multas automáticas ni calificación algorítmica |
| S20 | Media | ¿Cuál es el calendario institucional de feriados, excepciones y reservas de espacios? | Administrador configura días no operativos y horarios por tipo de recurso |
| S21 | Media | ¿Cómo se importará el inventario ya existente? | Carga inicial controlada a partir de datos facilitados por COCOA y posterior edición manual |
| S22 | Media | ¿Cuál es el presupuesto y el proveedor aprobado de infraestructura y correo? | Usar servicios con planes de desarrollo y costos explícitos; no fijar presupuesto hasta confirmación |
| S23 | Media | ¿Cuánto tiempo se conserva el historial, quién puede exportarlo y cómo se atienden solicitudes de datos personales? | Acceso limitado a administradores y conservación mínima necesaria; política de retención por definir con COCOA/USFQ |
| S24 | Baja | ¿Cómo se notifican al administrador revisiones periódicas del inventario? | Dashboard de estados disponible en todo momento; correos de resumen semanales quedan como mejora futura |

**No inferir como hechos:** horarios exactos para devoluciones, prioridad real de las solicitudes pendientes, multas, valoración por estrellas, infraestructura final, régimen de aprobación parcial o automatización de no retiro.

## 8. Épicas del MVP

| Épica | Qué cubre | Funcionalidades del §3 |
| --- | --- | --- |
| **E1 · Identidad y permisos** | Acceso Microsoft, habilitación por COCOA, roles, usuarios y restricciones | 1–2, 20 |
| **E2 · Catálogo y reservas** | Exploración, fichas, calendario, carrito, checkout, cancelación y consulta personal | 3–7, 10–11, 18 |
| **E3 · Aprobación y comunicaciones** | Revisión administrativa, confirmaciones y recordatorios por correo | 8–9, 12–13 |
| **E4 · Inventario y ciclo del préstamo** | Administración del catálogo, disponibilidad, checklist de salida, devolución e incidencias | 14–17 |
| **E5 · Comprobantes, reportes y auditoría** | Exportaciones, seguimiento e historial operativo protegido | 19–20 |

Las historias de usuario, criterios de aceptación detallados y tareas por épica se prepararán en el avance 3.

## 9. Criterios de éxito y restricciones

### Criterios de éxito verificables

1. Un usuario institucional **sin habilitación** no puede crear ni consultar reservas ajenas, incluso si inició sesión correctamente con Microsoft.
2. Un usuario habilitado puede encontrar un artículo, consultar fechas y enviar una solicitud con varios recursos desde móvil o escritorio, sin intervención manual previa del administrador.
3. Al enviar una solicitud se muestra **Pendiente de aprobación**, se registra una sola vez y el administrador recibe el aviso correspondiente.
4. El administrador puede aprobar o rechazar desde el panel; ninguna reserva pendiente aparece como aprobada antes de la decisión humana.
5. El sistema rechaza una aprobación que produciría un conflicto de disponibilidad con otra reserva o con mantenimiento.
6. Los recordatorios se programan para **T−30 minutos de inicio** y **T−30 minutos de devolución** de una reserva aprobada; cancelarla evita avisos futuros. En pruebas se verifican ejecución y registro de intentos de entrega.
7. Un administrador puede marcar, ítem por ítem, qué se entregó y qué se devolvió, consultar el registro y dejar fuera de disponibilidad un artículo dañado o extraviado.
8. Un usuario puede consultar sus propias reservas e historial; un administrador puede localizar una reserva y generar sus comprobantes o reportes sin hojas de seguimiento manuales.
9. Los controles de acceso se verifican en API y base de datos; ningún usuario no autorizado accede a información de otros por manipular URL o peticiones.
10. Las principales pantallas son navegables por teclado, muestran errores comprensibles y mantienen contraste de texto de al menos **4.5:1**.

### Restricciones y condiciones de implementación

- **Segundo avance documental:** miércoles **25 de noviembre de 2026, 23:59**. Se entrega un repositorio GitHub accesible al docente que incluya `docs/prd/prd.md`, `docs/diseno/brand-board.html`, `DESIGN.md` y `README.md`.
- **Primera entrega funcional comunicada en clase:** **2 de diciembre de 2026**. La fecha exacta de la presentación final deberá verificarse con el profesor.
- **Equipo:** dos integrantes, Juanes Vargas y Ailyn León.
- **Tecnología:** sin stack obligatorio. Se evaluará una arquitectura con frontend adaptable, backend con validación en servidor, base de datos relacional o equivalente con garantías transaccionales, autenticación Microsoft y un mecanismo confiable de trabajos programados para correos. **Supabase es una opción planteada en las notas, no una obligación tecnológica confirmada.**
- **Seguridad:** configuración de secretos fuera del repositorio, cifrado en tránsito, permisos basados en roles y políticas de acceso a datos, validación del lado del servidor, auditoría de acciones sensibles y protección contra dobles aprobaciones.
- **Datos:** mantener el catálogo existente, pero el formato de importación y la disponibilidad de fotografías, identificadores y unidades aún deben confirmarse.
- **Diseño:** identidad COCOA/USFQ según el moodboard del equipo: blanco `#FFFFFF`, negro `#000000`, carbón `#1E1E1E` y rojo `#D81C22`; lenguaje editorial con Archivo Black, University Roman e Inter, y Liquid Glass aplicado de forma selectiva a controles flotantes. Los tokens, componentes, contrastes y ejemplos quedarán definidos en el brand board y `DESIGN.md`.
- **Accesibilidad y rendimiento:** el efecto Liquid Glass no puede reducir legibilidad ni bloquear la interacción; se proporcionarán superficies opacas cuando sea necesario y se respetarán preferencias de movimiento reducido.
- **Despliegue y presupuesto:** proveedor, dominio, costos, volumen de correo y política de retención pendientes de acuerdo con la universidad.

## Uso de IA

El equipo utilizó **ChatGPT** para organizar el brief del primer avance, sintetizar las notas de la visita del cliente, identificar reglas ambiguas y casos límite, estructurar este PRD según la consigna y analizar la dirección de arte del moodboard. Las decisiones comunicadas en clase y las aclaraciones del equipo se distinguen de los supuestos; las preguntas sin respuesta se mantienen abiertas. **El equipo debe revisar y validar este documento antes de su publicación y uso por agentes de desarrollo.**

---

**Control de coherencia para los siguientes entregables:** `DESIGN.md` y `brand-board.html` deben representar los estados de reserva (pendiente, aprobada, en préstamo, devuelta, rechazada, cancelada y atrasada), los estados del inventario y los estados de interfaz (cargando, vacío, error y éxito), manteniendo el mismo texto y significado de este PRD. No asignar un color al estado «disponible» como si fuera sinónimo de «aprobada».
