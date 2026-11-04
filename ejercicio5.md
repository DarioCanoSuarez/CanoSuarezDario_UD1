# E05 · Un sprint en un tablero

## Ficha de la metodología

| Campo | Descripción |
|---|---|
| **Metodología elegida** | Scrum |
| **Principios clave** | Desarrollo iterativo e incremental en ciclos cortos llamados sprints (1 a 4 semanas). Se basa en la transparencia del trabajo, la inspección continua del producto/proceso y la rápida adaptación ante cambios de requisitos o prioridades. |
| **Roles clave** | **Product Owner**: Representa al cliente, define los requisitos, gestiona y prioriza la pila de producto (*Product Backlog*).<br>**Scrum Master**: Facilita el proceso, asegura que el equipo siga los principios de Scrum y elimina los impedimentos que bloqueen el trabajo.<br>**Equipo de Desarrollo**: Equipo multidisciplinar y autoorganizado que diseña, programa y prueba para entregar un incremento funcional al final de cada sprint. |
| **Eventos / Artefactos** | **Eventos**: Sprint Planning (planificación), Daily Scrum (reunión diaria de 15 min), Sprint Review (demostración del incremento) y Sprint Retrospective (mejora continua).<br>**Artefactos**: Product Backlog (pila del producto), Sprint Backlog (pila del sprint) e Incremento (software funcionando). |
| **Cuándo encaja** | Proyectos donde los requisitos no están totalmente definidos al inicio, son propensos a cambios frecuentes o se necesita entregar valor operativo y funcional rápidamente al cliente para validar el producto. |
| **Cuándo no encaja** | Proyectos estrictamente cerrados en alcance y presupuesto donde no cabe ningún cambio, o en organizaciones con estructuras jerárquicas rígidas que impidan la autoorganización del equipo y la comunicación fluida. |
| **Fuentes** | 1. *La Guía de Scrum (Scrum Guide)* - [https://scrumguides.org/scrum-guide.html](https://scrumguides.org/scrum-guide.html) (Consultado: 04/11/2026)<br>2. *Agile Alliance - What is Scrum?* - [https://www.agilealliance.org/glossary/scrum](https://www.agilealliance.org/glossary/scrum) (Consultado: 04/11/2026) |

---

## Historias de usuario

### H1: Reserva de tramo horario por parte del vecino
* **Estimación**: 3 puntos de historia

```text
Como vecino,
quiero seleccionar una pista y un tramo horario de una hora entre las 9:00 y las 22:00,
para reservar una pista desde mi ordenador o móvil sin tener que acudir presencialmente ni llamar por teléfono.
```

**Criterios de aceptación:**
```text
Dado que un vecino está autenticado y consulta el cuadrante de una pista en una fecha dada,
Cuando selecciona un tramo disponible de 1 hora entre las 9:00 y las 22:00 y confirma la reserva,
Entonces el sistema guarda la reserva y muestra una confirmación en pantalla marcando esa pista y hora como ocupadas.

Dado que un tramo horario ya ha sido reservado previamente por otro usuario,
Cuando un vecino intenta seleccionar ese mismo tramo y pista,
Entonces el sistema muestra el tramo bloqueado/deshabilitado y no permite tramitar la reserva.
```

---

### H2: Control del límite de dos reservas pendientes
* **Estimación**: 2 puntos de historia

```text
Como vecino,
quiero que el sistema me permita tener un máximo de dos reservas activas simultáneamente,
para garantizar un acceso equitativo a las pistas entre todos los ciudadanos.
```

**Criterios de aceptación:**
```text
Dado que un vecino tiene una sola reserva pendiente en el sistema,
Cuando intenta realizar una nueva reserva dentro del horario permitido,
Entonces el sistema procesa la solicitud correctamente y registra la segunda reserva.

Dado que un vecino ya tiene dos reservas pendientes registradas a su nombre,
Cuando intenta realizar una tercera reserva,
Entonces el sistema rechaza la operación y muestra un mensaje informando de que ha alcanzado el límite máximo permitido.
```

---

### H3: Panel de ocupación diaria para el personal de mostrador
* **Estimación**: 3 puntos de historia

```text
Como empleado del mostrador del polideportivo,
quiero ver un panel con la ocupación de todas las pistas a lo largo del día actual,
para atender las dudas de los usuarios en el centro y saber en todo momento qué pistas están ocupadas o libres.
```

**Criterios de aceptación:**
```text
Dado que el empleado del mostrador accede a la sección de administración diaria,
Cuando selecciona el día actual,
Entonces el sistema despliega un cuadrante completo con las pistas de pádel, tenis y fútbol sala y su estado hora a hora.

Dado que una pista se encuentra libre en una hora concreta,
Cuando el empleado revisa el panel,
Entonces la celda correspondiente se muestra en verde con la etiqueta "Libre" e indica la opción de registrar un uso presencial.
```

---

### H4: Aplicación de precio reducido para empadronados
* **Estimación**: 3 puntos de historia

```text
Como vecino empadronado en la localidad,
quiero que el sistema reconozca mi condición de residente al introducir mi DNI,
para beneficiarme del precio reducido asignado a los empadronados al tramitar la reserva.
```

**Criterios de aceptación:**
```text
Dado que un usuario empadronado introduce su DNI durante el proceso de reserva,
Cuando el sistema valida su número con el registro municipal,
Entonces se aplica automáticamente la tarifa bonificada antes de confirmar la reserva.

Dado que un usuario no empadronado introduce un DNI no registrado en la base de datos municipal,
Cuando el sistema comprueba la identidad,
Entonces aplica el precio general estándar e informa del motivo en el desglose del importe.
```

---

### H5: Consulta y cancelación de reservas pendientes
* **Estimación**: 2 puntos de historia

```text
Como vecino,
quiero ver el listado de mis reservas pendientes y poder cancelar una de ellas si no voy a poder ir,
para liberar la pista a otros vecinos y recuperar el cupo que me permite hacer otra reserva.
```

**Criterios de aceptación:**
```text
Dado que un usuario accede a su apartado "Mis reservas",
Cuando selecciona una reserva futura y pulsa en "Cancelar reserva",
Entonces el sistema anula la reserva, la pista vuelve a quedar disponible en el cuadrante y libera el cupo del usuario.

Dado que el tramo reservado está a punto de comenzar (quedan menos de 15 minutos),
Cuando el usuario pulsa el botón de cancelar,
Entonces el sistema rechaza la cancelación indicando que ha expirado el plazo límite permitido.
```

---

## Pila del producto (Product Backlog)

| Orden | ID | Historia de usuario | Puntos | Justificación |
|---|---|---|---|---|
| 1 | **H1** | Reserva de tramo horario por parte del vecino | 3 | Es la funcionalidad central del sistema. Sin la capacidad básica de reservar tramos no existe producto funcional ni valor posible. |
| 2 | **H2** | Control del límite de dos reservas pendientes | 2 | Resuelve uno de los problemas prioritarios planteados por el Ayuntamiento: el uso injusto y las ausencias en las pistas. |
| 3 | **H3** | Panel de ocupación diaria para el personal de mostrador | 3 | Proporciona visibilidad operativa inmediata al personal del centro para la gestión del día a día de las instalaciones. |
| 4 | **H5** | Consulta y cancelación de reservas pendientes | 2 | Permite liberar pistas sin usar, combatiendo el ausentismo, aunque depende de tener antes funcional el sistema de reservas (H1). |
| 5 | **H4** | Aplicación de precio reducido para empadronados | 3 | Aporta valor económico pero requiere integraciones/validaciones de datos adicionales y se puede postergar sin bloquear el flujo básico de uso. |

---

## Primer sprint

* **Objetivo del sprint**: Permitir a los vecinos realizar reservas de pistas por tramos de una hora respetando el límite de dos reservas activas por persona, y facilitar al personal del polideportivo la visualización del cuadrante diario de ocupación.
* **Historias seleccionadas**: 
  - **H1**: Reserva de tramo horario por parte del vecino (3 pts)
  - **H2**: Control del límite de dos reservas pendientes (2 pts)
  - **H3**: Panel de ocupación diaria para el personal de mostrador (3 pts)
  - **Total de puntos**: **8 puntos de historia** (capacidad exacta del equipo para el sprint).

### Definición de Terminado (*Definition of Done - DoD*)
Una historia de usuario se considerará completada y lista para entrega únicamente cuando:
1. El código fuente haya sido revisado y aprobado mediante *pull request* por otro desarrollador del equipo y no contenga errores de compilación ni advertencias.
2. Se hayan ejecutado y superado las pruebas (unitarias y de integración) para todos los criterios de aceptación (casos normales y límite).
3. La funcionalidad esté desplegada en el entorno de pruebas y validada funcionalmente.

---

## Preguntas

1. **¿Qué ventajas tiene estimar las historias en puntos de historia en lugar de horas de trabajo?**  
   Los puntos de historia estiman la complejidad relativa, el esfuerzo y la incertidumbre de una tarea global sin depender de las habilidades de un desarrollador en particular. Las estimaciones en horas cambian según quién programe la tarea, mientras que los puntos de historia se mantienen estables para todo el equipo y permiten calcular la velocidad real del grupo a lo largo de los sprints.

2. **¿Por qué las historias de usuario deben escribirse pensando en el usuario final y no en las tareas técnicas de programación?**  
   Porque las historias expresan qué necesita el cliente y qué valor de negocio le aporta ("qué" y "para qué"), permitiendo al Product Owner priorizar adecuadamente. Las tareas de programación son detalles de implementación técnica ("cómo") que corresponden decidir al equipo de desarrollo y que carecen de significado funcional por sí solas para el cliente.

3. **¿Qué ocurriría si durante la Sprint Planning el equipo decide aceptar 12 puntos de historia sabiendo que su capacidad es de 8 puntos?**  
   Se generaría un sobrecompromiso no realista que provocaría presión innecesaria, devaluación de la calidad del código (deuda técnica) y una alta probabilidad de no cumplir el objetivo del sprint. En Scrum, dejar historias a medias al final del sprint equivale a entregar 0 incremento funcional completado sobre esas tareas.
