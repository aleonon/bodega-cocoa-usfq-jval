# Revisión adversarial del PRD — Bodega COCOA

> **Fecha:** 23 de noviembre de 2026  
> **Equipo:** Juanes Vargas y Aylin León  
> **PRD revisado:** `docs/prd/prd.md`, versión 1.1  
> **Base de comparación:** PRD v1.0 del 22 de noviembre de 2026, notas del cliente (Entrevista.pdf, pp. 3–5) y decisiones expresas del equipo del 23 de noviembre.

## Método y jerarquía de fuentes

La revisión sigue la guía «Del PRD generado al PRD revisado»: identificar huecos, registrar frases del borrador, contrastar fuentes y corregir sin presentar suposiciones como hechos. La fuente de mayor autoridad son las respuestas del cliente anotadas en clase; las decisiones posteriores del equipo son **provisionales** y aparecen en el PRD §6 como E23-01 a E23-08 y §7 como supuestos.

**Atribución de hallazgos:** los cinco primeros huecos se identificaron en la revisión guiada y los tres últimos se profundizaron con análisis adversarial de IA. La clasificación «Equipo»/«IA» describe la procedencia de esta revisión asistida; antes de entregarla, Juanes y Aylin deben confirmar que refleja el trabajo real de ambos.

## Huecos y correcciones

| # | Sección | Qué decía exactamente el PRD v1.0 | Tipo de hueco | Gravedad | Quién lo encontró | Corrección aplicada en v1.1 |
| --- | --- | --- | --- | --- | --- | --- |
| R-01 | §4.3 reglas 21–24 / §7 S01 | «La solicitud pendiente **no consume definitivamente** inventario; la disponibilidad se revalida al aprobar» | Supuesto incompatible con decisión del equipo | Alta | Equipo | Se cambió a **retención temporal de unidades desde envío** hasta decisión, cancelación o vencimiento al inicio; las retenciones incompatibles no pueden coexistir. §4.3 y §7 S01/S26. Pendiente de ratificación del cliente. |
| R-02 | §3 función 6 / §4.3 regla 12 | «agregar varios artículos y/o espacios a una solicitud, revisar cantidades y fechas» | Regla ambigua / ausencia de ventana temporal | Alta | Equipo | Una misma fecha y hora de inicio y fin para **todos los artículos del carrito**. §3 función 6, §4.3 regla 12 y §7 S25. Pendiente de confirmación del cliente. |
| R-03 | §4.3 regla 24 / §7 S02 | «Aprobar o rechazar la solicitud completa; si falta algo, solicitar nueva selección antes de aprobar» | Supuesto incompatible con decisión del equipo / caso borde | Alta | Equipo | Se permite **aprobación parcial por unidad**, correo con desglose, retención solo de aprobados y liberación de rechazados. §4.3 reglas 23–24, §7 S02/S27. Se mantiene pendiente el consentimiento a modificaciones. |
| R-04 | §4.4 regla 28 / §7 S14 | «la lista deberá reflejar los ítems efectivamente entregados, incluso ante una entrega incompleta» | Estado y validación incompletos | Alta | Equipo | Checklist por **unidad**, estado entregada/faltante, motivo y responsable, sin exigir devolución de lo nunca entregado. §4.4 regla 29, §7 S14. Falta confirmar evidencia adicional. |
| R-05 | §4.3 regla 15 / §7 S05 | «el último turno válido queda pendiente de confirmación» | Regla sin cifra / incompatibilidad horaria | Alta | Equipo | Supuesto operativo: turnos de 30 min desde 08:30, **último inicio 17:00**; **17:20** cierre administrativo. §4.3 regla 15, §7 S05. No se presume hora máxima de devoluciones; cliente debe ratificar. |
| R-06 | §4.4 regla 32 / §7 S07-S08 | «Vencida / con devolución atrasada» | Estados confundidos / falta de transición | Media | IA (análisis adversarial) | Se diferencia **solicitud pendiente vencida al inicio** (automática: cierra/libera) de **devolución atrasada** (indicador de equipos entregados que siguen ocupados). §4.3 regla 26, §4.4 regla 33 y §7 S07–S08. Se requiere validación del cliente. |
| R-07 | §4.3 regla 27 / §7 S08 | «Los recordatorios automáticos se envían 30 minutos antes del inicio previsto» | Caso borde de notificación | Media | IA (análisis adversarial) | Si se aprueba después de T−30, se envía **confirmación inmediata**, pero no recordatorio de inicio retroactivo. §4.3 regla 28 y §7 S17. No afecta recordatorio de devolución si aún corresponde. |
| R-08 | §3 función 19 / §9 criterios | «ofrecer un comprobante por reserva y exportación de datos de reservas en Excel y PDF para la administración» | Alcance inflado para hito intermedio | Media | IA (análisis adversarial) | Se prioriza demo **2 dic** con flujo de reservas y control administrativo; **reportes avanzados y Excel/PDF después del hito**, aún dentro del alcance final. §3 intro/19, §5 y §9. Falta validación de prioridades con cliente/profesor. |

## Decisiones validadas por el equipo (no por el cliente)

| ID | Decisión | Origen |
| --- | --- | --- |
| E23-01 | Retener inventario mientras una solicitud está pendiente | R-01 |
| E23-02 | Una misma fecha y horario para el carrito completo | R-02 |
| E23-03 | Permitir aprobación parcial | R-03 |
| E23-04 | Checklist por unidad y faltantes | R-04 |
| E23-05 | Último turno 17:00 / cierre 17:20 | R-05 |
| E23-06 | Vencimiento al inicio de solicitudes todavía pendientes | R-06 |
| E23-07 | Confirmación inmediata sin recordatorio vencido | R-07 |
| E23-08 | Priorizar demo operativa y posponer reporting avanzado | R-08 |

## Riesgos que permanecen abiertos

- **Bloqueos prolongados:** la retención se mantiene hasta aprobación/rechazo/cancelación/inicio. Para reservas con inicio muy lejano, el inventario podría estar apartado demasiado tiempo. Confirmar un SLA o plazo máximo de revisión (PRD S26).
- **Aceptación de reservas parciales:** decidir si el solicitante debe aceptar cambios en cantidades o sustituciones (PRD S27).
- **Horarios:** validar si 17:00 es el último retiro y cuál es la última devolución admisible (PRD S05).
- **Reservas aprobadas no retiradas:** no se vencen automáticamente; necesitan política de liberación administrativa (PRD S07).
- **Entregas parciales:** confirmar si hacen falta firmas, fotos o soporte del estudiante en el checklist (PRD S14).

## Para presentar (aproximadamente 1 minuto)

### 1. R-01 — Retenciones del inventario · Equipo

**Qué decía:** las solicitudes pendientes no bloqueaban definitivamente el inventario. **Por qué era un problema:** permitía que varias solicitudes compitieran por la misma cámara y complicaba asegurar disponibilidad real. **Cómo quedó:** ahora se aparta temporalmente al enviar y se libera al decidir, cancelar o vencer; falta ratificación del cliente sobre el plazo máximo.

### 2. R-03 — Aprobaciones parciales · Equipo

**Qué decía:** la solicitud debía aprobarse o rechazarse completa. **Por qué era un problema:** no contemplaba que el administrador tuviera que negar solo una cámara y entregar las demás. **Cómo quedó:** puede aprobar por unidad, mostrar el desglose y liberar únicamente lo rechazado; falta confirmar la aceptación de modificaciones.

### 3. R-06 — Solicitudes sin respuesta · IA (análisis adversarial)

**Qué decía:** «Vencida / con devolución atrasada» estaba unido en una misma definición. **Por qué era un problema:** podía confundir una solicitud nunca aprobada con un equipo prestado que se devolvió tarde. **Cómo quedó:** la solicitud pendiente vence al llegar su inicio y libera recursos, mientras un préstamo atrasado sigue ocupando inventario.

## Verificaciones de consistencia

- El carrito **sin enviar** vence a la hora; la **retención de una solicitud enviada** es distinta y no se libera por la caducidad del carrito.
- La aprobación manual sigue siendo obligatoria, incluso si los recursos están temporalmente apartados.
- «Vencida» se aplica a solicitudes **pendientes** al llegar la hora inicial, no a reservas aprobadas.
- «Devolución atrasada» no libera inventario por sí sola.
- La aprobación parcial obliga a que el checklist y la devolución comprendan **solo las unidades efectivamente aprobadas y entregadas**.
- Los ocho ajustes son decisiones **provisionales del equipo**; todavía pueden cambiar después de la ratificación del cliente.

## Uso de IA

Se utilizó ChatGPT para comparar el PRD v1.0 con la guía y las notas conocidas, localizar casos borde, proponer correcciones y redactar este registro. Las decisiones E23-01 a E23-08 fueron seleccionadas explícitamente por el equipo en la conversación del 23 de noviembre. La aprobación formal del cliente queda pendiente.
