# Creacion de User Stories para LTI ATS

---

## User Story 1: Crear y publicar vacante con multiposting

* **Como** reclutador de una agencia de selección,
* **quiero** crear una vacante y publicarla automáticamente en varios portales de empleo,
* **para** ahorrar tiempo y centralizar todas las candidaturas en un solo lugar.

### Descripción

Carolina, reclutadora senior en una agencia en Bogotá, necesita abrir una nueva vacante para un desarrollador backend. Hoy pierde tiempo repitiendo el mismo contenido en diferentes portales. Con LTI ATS, ella crea la vacante una sola vez, define los requisitos y, con un clic, la publica en varios portales de empleo, manteniendo trazabilidad de dónde llegaron los candidatos y concentrando todas las postulaciones en el sistema. 

### Criterios de aceptación (Gherkin)

**Scenario 1: Creación básica de vacante**

* **Dado que** soy un reclutador autenticado en LTI ATS
* **y** tengo permisos para crear vacantes para mi empresa
* **cuando** accedo a la sección "Nueva vacante"
* **y** completo los campos obligatorios (título, descripción, ubicación, tipo de contrato, requisitos mínimos)
* **y** guardo la vacante como "Borrador"
* **entonces** la vacante debe quedar registrada en estado "Borrador"
* **y** debo ver la vacante en la lista de vacantes de mi empresa.

---

**Scenario 2: Publicación de vacante en LTI ATS**

* **Dado que** tengo una vacante en estado "Borrador" con todos los campos obligatorios completos
* **cuando** selecciono la opción "Publicar"
* **entonces** el sistema debe cambiar el estado de la vacante a "Abierta"
* **y** la vacante debe ser visible en el portal de candidatos de LTI ATS.

---

**Scenario 3: Multiposting a portales externos**

* **Dado que** tengo una vacante en estado "Abierta"
* **y** la cuenta de mi empresa tiene configuradas integraciones con uno o más portales de empleo
* **cuando** selecciono los portales donde quiero publicar y confirmo la acción
* **entonces** el sistema debe enviar la información de la vacante a los portales seleccionados
* **y** mostrarme un mensaje de confirmación con el resultado por portal (éxito/error).

---

**Scenario 4: Trazabilidad de orígenes de candidatura**

* **Dado que** una vacante ha sido publicada tanto en el portal LTI como en portales externos
* **cuando** un candidato se postula desde cualquiera de los canales
* **entonces** la postulación debe crearse en LTI ATS asociada a la vacante
* **y** el registro debe incluir el canal de origen (por ejemplo: "Portal LTI", "Computrabajo", "LinkedIn").

---

**Scenario 5: Validación de campos obligatorios**

* **Dado que** estoy creando o editando una vacante
* **cuando** intento guardar la vacante sin completar los campos obligatorios
* **entonces** el sistema debe impedir el guardado
* **y** mostrar mensajes de error específicos junto a los campos faltantes.

### Priorización

* **Prioridad**: Alta (core para el MVP, habilita el flujo completo de reclutamiento)
* **Esfuerzo estimado**: L (incluye lógica de negocio + UI + integraciones básicas de multiposting)

### Notas adicionales

* El diseño debe seguir buenas prácticas de UX para formularios largos (secciones, ayudas contextuales, campos sugeridos).
* La estructura de la vacante debe ser compatible con lo que requiere el módulo de IA para el matching (requisitos, palabras clave, nivel de experiencia). 
* La integración con portales de empleo puede empezar con uno o dos portales como “pilot” y extensible via configuración.

### Tareas

1. **Diseño funcional y UX**

   * Definir campos mínimos y avanzados de la vacante (obligatorios vs opcionales).
   * Diseñar wireframes de pantalla de creación/edición de vacantes.
   * Definir mensajes de error y ayudas contextuales.

2. **Back-end**

   * Crear modelo de datos de Vacante (si no existe) y endpoints para:

     * Crear, editar, listar, cambiar estado.
   * Implementar lógica de cambio de estado (Borrador, Abierta, Cerrada).
   * Implementar servicio de multiposting con interfaz genérica para diferentes portales.

3. **Integraciones**

   * Implementar adaptadores para 1–2 portales de empleo iniciales.
   * Manejar respuestas de éxito/error y logs de integración.

4. **Front-end**

   * Implementar formularios de creación/edición de vacante.
   * Implementar listado de vacantes con indicadores de estado y canales publicados.
   * Implementar flujo de multiposting (selección de portales, feedback visual).

5. **Seguridad & permisos**

   * Validar que solo usuarios con rol RECLUTADOR/ADMIN puedan crear o editar vacantes de su empresa.

6. **Pruebas**

   * Pruebas unitarias en back-end y front-end.
   * Pruebas de integración con portales de empleo.
   * Pruebas de UX con 1–2 reclutadores reales.

---

## User Story 2: Panel de candidatos con ranking inteligente (IA)

* **Como** reclutador,
* **quiero** ver un listado de candidatos para una vacante ordenado por un puntaje de adecuación calculado por IA,
* **para** priorizar rápidamente a quién revisar y avanzar en el proceso.

### Descripción

Andrés gestiona más de 100 CVs por vacante. Sin ayuda, revisar todo es inviable. El módulo de IA de LTI ATS analiza los CVs, extrae la información relevante y genera un puntaje de ajuste para cada vacante. En el panel de candidatos, Andrés ve un ranking donde primero aparecen los candidatos con mayor probabilidad de encajar, con filtros y acciones rápidas para avanzar de fase o descartar. 

### Criterios de aceptación (Gherkin)

**Scenario 1: Visualización de candidatos con puntaje IA**

* **Dado que** soy un reclutador autenticado
* **y** existe una vacante con varias postulaciones
* **cuando** accedo al detalle de la vacante
* **entonces** debo ver una lista de candidatos asociados a esa vacante
* **y** cada candidato debe mostrar al menos: nombre, fecha de postulación, estado actual, puntaje IA (0–100) y canal de origen.

---

**Scenario 2: Orden por puntaje IA por defecto**

* **Dado que** estoy viendo la lista de candidatos para una vacante
* **cuando** no he aplicado ningún filtro ni orden personalizado
* **entonces** la lista debe estar ordenada de mayor a menor puntaje IA por defecto.

---

**Scenario 3: Actualización de puntajes IA**

* **Dado que** el motor de IA ha recalculado los puntajes (por cambios en la vacante o nuevas postulaciones)
* **cuando** vuelvo a abrir el panel de candidatos de la vacante
* **entonces** debo ver los puntajes actualizados
* **y** el orden de la lista debe reflejar los nuevos puntajes.

---

**Scenario 4: Filtro por estado y puntaje mínimo**

* **Dado que** estoy viendo la lista de candidatos
* **cuando** aplico un filtro de "estado = Recibida"
* **y** defino un puntaje mínimo (por ejemplo, ≥ 70)
* **entonces** la lista solo debe mostrar candidatos con estado "Recibida"
* **y** con puntaje IA mayor o igual al valor mínimo.

---

**Scenario 5: Acceso rápido a detalles del candidato**

* **Dado que** estoy viendo la lista de candidatos
* **cuando** hago clic en un candidato
* **entonces** el sistema debe mostrar el detalle del candidato, incluyendo CV estructurado, experiencia, habilidades y cualquier información relevante introducida por la IA.

### Priorización

* **Prioridad**: Alta (es uno de los diferenciales clave de LTI ATS frente a ATS tradicionales).
* **Esfuerzo estimado**: L (implica integración con módulo IA + UI avanzada).

### Notas adicionales

* El puntaje IA debe ser interpretable (tooltip o breakdown simple: principales criterios que influyeron en la puntuación). 
* La primera versión puede limitarse a un modelo sencillo de matching por palabras clave, experiencia y requisitos mínimos.
* Debe existir un fallback razonable cuando la IA no pueda calcular puntaje (ej. candidato sin CV o formato ilegible).

### Tareas

1. **Diseño funcional**

   * Definir rango del puntaje (0–100) y cómo se muestra visualmente (barra, chip, color).
   * Definir filtros disponibles (estado, puntaje mínimo, fecha de postulación, canal).

2. **Back-end**

   * Extender la entidad Aplicación con campo `puntajeIA`.
   * Crear endpoints para:

     * Obtener candidatos por vacante con paginación y criterios de orden.
   * Integrar con el módulo de IA (servicio de scoring).

3. **Módulo IA**

   * Implementar endpoint que reciba datos de candidato + vacante y devuelva `puntajeIA`.
   * Manejar errores y tiempos de respuesta (time-out, reintentos).

4. **Front-end**

   * Implementar panel de candidatos en el detalle de la vacante.
   * Implementar ordenamiento por puntaje, nombre, fecha.
   * Implementar filtros (estado, puntaje mínimo, canal).

5. **Pruebas**

   * Pruebas unitarias de cálculo de puntaje (en IA) con casos de ejemplo.
   * Pruebas de integración para asegurar que al llegar una nueva candidatura se dispara el cálculo de puntaje.
   * Pruebas de usabilidad con reclutadores: validación de utilidad del ranking.

---

## User Story 3: Programación automática de entrevistas con integración de calendario

* **Como** reclutador,
* **quiero** programar entrevistas con candidatos desde el ATS consultando la disponibilidad de los entrevistadores,
* **para** reducir el intercambio de correos y confirmar rápidamente una fecha y hora.

### Descripción

Laura coordina entrevistas entre candidatos y gerentes de contratación. Actualmente, intercambia múltiples correos para encontrar una franja horaria. Con LTI ATS, desde la propia aplicación, ella selecciona a los candidatos preseleccionados, define los entrevistadores y el tipo de entrevista. El sistema consulta la disponibilidad en los calendarios externos (Google/Outlook) y propone franjas posibles. Una vez seleccionada una franja, se envían invitaciones y recordatorios automáticos. 

### Criterios de aceptación (Gherkin)

**Scenario 1: Propuesta de franjas horarias**

* **Dado que** soy un reclutador autenticado
* **y** tengo integraciones de calendario configuradas para los entrevistadores
* **cuando** abro el flujo "Programar entrevista" para un candidato y una vacante
* **y** selecciono a los entrevistadores requeridos
* **entonces** el sistema debe consultar la disponibilidad en los calendarios configurados
* **y** mostrar un listado de franjas horarias posibles dentro del rango de fechas que especifiqué.

---

**Scenario 2: Creación de la entrevista e invitaciones**

* **Dado que** ya seleccioné una franja horaria propuesta
* **cuando** confirmo la creación de la entrevista
* **entonces** el sistema debe crear un registro de Entrevista en LTI ATS
* **y** crear eventos en los calendarios de entrevistadores y candidato (si se dispone de email)
* **y** enviar invitaciones por correo electrónico con los detalles (fecha, hora, tipo, enlace de videollamada si aplica).

---

**Scenario 3: Confirmación del candidato**

* **Dado que** se ha enviado la invitación al candidato
* **cuando** el candidato hace clic en el enlace de confirmación
* **entonces** el sistema debe marcar la entrevista como "Programada / Confirmada"
* **y** registrar la fecha y hora de confirmación.

---

**Scenario 4: Reprogramación de entrevista**

* **Dado que** existe una entrevista programada
* **cuando** el reclutador elige la opción "Reprogramar"
* **entonces** el sistema debe volver a consultar la disponibilidad en los calendarios de los participantes
* **y** permitir seleccionar una nueva franja
* **y** actualizar los eventos de calendario e invitaciones asociadas.

### Priorización

* **Prioridad**: Media-Alta (clave para eficiencia, pero posterior a creación de vacantes y panel de candidatos).
* **Esfuerzo estimado**: XL (integraciones de calendario + lógica de reprogramación + UI específica).

### Notas adicionales

* En una primera iteración, se puede empezar con una integración a un solo proveedor de calendario (por ejemplo Google Calendar). 
* Las invitaciones deberían incluir un enlace único para que el candidato confirme o solicite cambio.
* Deben registrarse los cambios para métricas de “no show” y reprogramaciones.

### Tareas

1. **Definición funcional**

   * Definir flujo detallado de programación y reprogramación.
   * Definir estados de la Entrevista (Programada, Realizada, Cancelada, Reprogramada).

2. **Back-end**

   * Crear endpoints para creación, actualización y cancelación de entrevistas.
   * Integrar con servicio de calendario (OAuth, tokens de acceso, etc.).

3. **Integraciones externas**

   * Implementar conector para Google Calendar (v1).
   * Manejo de errores de integración y mensajes claros al usuario.

4. **Front-end**

   * Implementar wizard de programación de entrevistas.
   * Vista de agenda/cronograma de entrevistas por vacante.

5. **Notificaciones**

   * Plantillas de correo para invitaciones, reprogramación y recordatorios.

6. **Pruebas**

   * Pruebas unitarias y de integración con el proveedor de calendario.
   * Pruebas de usabilidad con reclutadores.

---

## User Story 4: Portal de candidatos y postulación rápida con CV

* **Como** candidato,
* **quiero** postularme a una vacante enviando mi CV y datos básicos de forma rápida,
* **para** no perder tiempo rellenando formularios extensos y recibir confirmación inmediata de mi postulación.

### Descripción

Camila ve una vacante compartida por una agencia que usa LTI ATS. Cuando abre el enlace, llega a una página con la descripción clara del puesto y un formulario simple donde sube su CV, completa algunos datos esenciales y envía su postulación. El sistema extrae automáticamente la información principal del CV y crea su perfil de candidato. En segundos, Camila recibe un correo de confirmación y mensajes automatizados sobre los siguientes pasos. 

### Criterios de aceptación (Gherkin)

**Scenario 1: Postulación básica con CV**

* **Dado que** estoy en la página pública de una vacante de LTI ATS
* **cuando** completo mis datos mínimos (nombre, email)
* **y** adjunto un archivo de CV en un formato soportado (PDF, DOCX)
* **y** hago clic en "Postularme"
* **entonces** el sistema debe crear un registro de Candidato (si no existe)
* **y** crear una Aplicación asociada a la vacante
* **y** mostrar un mensaje de confirmación en pantalla.

---

**Scenario 2: Confirmación por correo al candidato**

* **Dado que** he enviado una postulación válida
* **cuando** el sistema procesa la candidatura
* **entonces** debe enviarme un correo de confirmación con:

  * nombre de la vacante
  * fecha y hora de postulación
  * información básica sobre próximos pasos.

---

**Scenario 3: Extracción automática de datos del CV**

* **Dado que** he subido un CV válido
* **cuando** la postulación es aceptada por el sistema
* **entonces** el módulo de IA debe intentar extraer datos clave (experiencia, estudios, habilidades)
* **y** guardarlos en el perfil estructurado del candidato.

---

**Scenario 4: Manejo de errores de formato de CV**

* **Dado que** intento subir un archivo en un formato no soportado
* **cuando** hago clic en "Postularme"
* **entonces** el sistema debe impedir el envío
* **y** mostrar un mensaje indicando los formatos aceptados.

### Priorización

* **Prioridad**: Alta (experiencia de candidato y entrada de datos al sistema dependen de esto).
* **Esfuerzo estimado**: M (formulario + back-end + integración inicial con módulo de parsing).

### Notas adicionales

* La página de vacante debe ser responsive y rápida, pensada también para móvil.
* Los campos mínimos deben ser configurables a nivel de empresa o vacante (por ejemplo, pedir teléfono o LinkedIn). 

### Tareas

1. **Front-end portal de candidatos**

   * Diseñar plantilla pública de vacante (detalles, beneficios, ubicación).
   * Implementar formulario simple de postulación.

2. **Back-end**

   * Endpoint público para crear candidatos y postulaciones.
   * Validación de formatos de archivo y tamaño máximo.

3. **Módulo IA / parsing**

   * Integrar con servicio de parsing de CV.
   * Guardar resultados en `perfilEstructurado` del candidato.

4. **Notificaciones**

   * Plantilla de correo de confirmación de postulación.
   * Configuración de remitente y branding por empresa.

5. **Pruebas**

   * Pruebas de carga básica (picos de postulaciones).
   * Pruebas en dispositivos móviles.


# Backlog completo de User Stories para LTI ATS

### Step 1–3: User Stories and Prioritization Matrix

| User Story                                                                         | Business/User Impact (High/Med/Low + reason)                                                                                                                                             | Urgency (High/Med/Low + reason)                                                                                                                                                                     | Implementation Complexity (High/Med/Low + reason)                                                                                                         | Risks & Dependencies                                                                                                                                                    |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **US1 – Recruiter login & secure access**                                          | **High** – Sin acceso seguro no hay forma de trabajar con datos de vacantes y candidatos; es el punto de entrada para reclutadores y empresas.                                           | **High** – Cualquier módulo interno (crear vacantes, ver candidatos) lo requiere; además, aunque se pueda mostrar algo público, para ventas demo B2B es crítico que el reclutador vea “su espacio”. | **Med** – Autenticación estándar (email + contraseña, roles básicos) y sesiones; no es trivial pero es una pieza muy conocida y reutilizable.             | - Depende de una decisión mínima sobre modelo de usuarios (empresa, reclutador).<br>- Riesgo bajo si se usa un enfoque estándar (JWT, proveedores externos, etc.).      |
| **US2 – Crear y gestionar vacantes (publicación en portal LTI, sin multiposting)** | **High** – Permite a la empresa publicar oportunidades reales y es el corazón de un ATS: sin vacantes, no hay candidatos ni proceso.                                                     | **High** – Es la primera funcionalidad funcional que “se ve” por fuera (páginas de vacantes públicas). Sin esto el producto no tiene sentido práctico.                                              | **Med** – Requiere modelo de vacante, formularios, estados básicos (borrador/abierta/cerrada) y listado interno; lógica manejable y muy acotable.         | - Depende de US1 para que un reclutador pueda crear/editar vacantes.<br>- Riesgo moderado de sobrediseñar el modelo de vacante; conviene empezar simple.                |
| **US3 – Portal de candidatos y postulación rápida con CV**                         | **High** – Entrega valor directo al usuario candidato y cierra el flujo completo: ver vacante → postularse. También genera datos reales (candidaturas) para el sistema.                  | **High** – Es clave para demostrar un “vertical slice” de producto (reclutador crea vacante / candidato aplica / reclutador ve la aplicación).                                                      | **Med** – Página pública, formulario simple, subida de CV y creación de candidato + aplicación. Complejidad media, bien conocida técnicamente.            | - Depende de US2 (vacantes públicas) para tener contenido que mostrar.<br>- Riesgo en manejo de archivos (tamaño, formatos) pero acotable con reglas simples.           |
| **US4 – Panel de candidatos por vacante con gestión de estados (pipeline básico)** | **High** – Es la razón por la que un reclutador paga un ATS: ver quién se ha postulado y mover personas a través del proceso (Recibido, En revisión, Entrevista, Rechazado, Contratado). | **High** – Sin esta vista, el sistema solo recibe CVs pero no ayuda a gestionar el proceso; imprescindible para demos creíbles y uso real.                                                          | **Med** – Listado, filtros simples, cambios de estado y registro de acciones. No requiere IA ni integraciones externas en la primera versión.             | - Depende de US1 (acceso) y US3 (existencia de postulaciones).<br>- Riesgo de complejidad si se intentan demasiados estados o automatismos de una vez.                  |
| **US5 – Ranking de candidatos con IA dentro del panel (scoring básico)**           | **High** – Es un diferenciador clave del producto y reduce el esfuerzo de revisión manual; da el “wow factor” en demos.                                                                  | **Med** – Importante para el posicionamiento del producto, pero no imprescindible para el primer uso funcional (el reclutador ya puede filtrar y gestionar sin IA).                                 | **High** – Requiere integrar un módulo de IA, definir features de entrada, manejar tiempos de respuesta y fallbacks cuando no se pueda calcular el score. | - Depende de US4 (panel de candidatos) y de tener datos mínimos de vacante + CV.<br>- Riesgo de calidad de modelo y explicabilidad de resultados; riesgo técnico mayor. |
| **US6 – Programación automática de entrevistas con integración de calendario**     | **Med** – Aporta eficiencia operativa, pero el reclutador puede seguir usando correo/calendario manualmente al inicio. Es un “nice-to-have fuerte”, no el core del ATS básico.           | **Med/Low** – Útil, pero no urgente para lanzar versión inicial: se puede incorporar en un release posterior como mejora clara.                                                                     | **High** – Integraciones con calendarios externos, manejo de permisos, reprogramaciones, enlaces únicos de confirmación; muchas piezas móviles.           | - Depende de US4 (candidatos en pipeline) para saber a quién invitar.<br>- Riesgo alto por integraciones externas y manejo de errores / permisos de calendario.         |
| **US7 – Multiposting de vacantes a portales de empleo externos**                   | **Med/High** – Para agencias y empresas con alto volumen, multiposting ahorra mucho tiempo y puede ser un argumento comercial fuerte, pero el sistema es útil incluso sin esto.          | **Med** – Aumenta el atractivo del producto, pero solo después de que el flujo básico de vacante–candidato–pipeline esté estable.                                                                   | **High** – Requiere integrar APIs diversas, manejar formatos distintos y estados de publicación; la complejidad crece con cada nuevo portal.              | - Depende de US2 (vacante creada) y de un modelo estable de vacante.<br>- Riesgo elevado por heterogeneidad de APIs externas y manejo de errores de publicación.        |

---

### Step 4: Reasoning (before ranking)

**US1 – Recruiter login & secure access**

* **Impact**: Sin login y contexto de empresa/reclutador, no hay entorno de trabajo seguro ni multi-tenant. Es imprescindible para cualquier operación interna y para cumplir expectativas mínimas de un SaaS B2B.
* **Urgency**: Alta porque todo lo demás (gestión de vacantes, panel de candidatos) asume un usuario autenticado. También es importante para mostrar a stakeholders un “dashboard de reclutador”.
* **Complexity**: Media; es una pieza técnica conocida (autenticación, roles básicos), pero puede escalar en complejidad si se añaden SSO, permisos avanzados, etc. Para MVP se puede recortar.
* **Influence on priority**: Debe ir primero para habilitar el resto del producto interno.

---

**US2 – Crear y gestionar vacantes (publicación en portal LTI, sin multiposting)**

* **Impact**: Es el core funcional: el producto existe para gestionar procesos de selección y eso empieza por tener vacantes. Además, da visibilidad externa (páginas públicas de vacante) y material real para demos.
* **Urgency**: Muy alta; no tiene sentido un ATS sin vacantes. Es crucial para mostrar un flujo de trabajo real: “entro, creo una vacante y se ve en la web”.
* **Complexity**: Media; diseño del modelo de vacante, formulario y estados básicos. Es bastante controlable si evitamos campos exóticos y reglas complejas al principio.
* **Influence on priority**: Debe seguir inmediatamente a la autenticación para construir la columna vertebral del sistema.

---

**US3 – Portal de candidatos y postulación rápida con CV**

* **Impact**: Cierra el círculo de valor: ya no solo se crean vacantes, sino que los candidatos pueden aplicar y generar datos reales. Esto permite mostrar el producto a ambos lados (reclutador y candidato).
* **Urgency**: Alta, porque sin candidatos no se justifica un ATS y, además, necesitamos generar datos para alimentar paneles e IA algunos pasos más adelante.
* **Complexity**: Media; requiere UI pública, validación de formularios, manejo de archivos y creación de registros de candidato/aplicación, pero todo dentro del dominio controlado.
* **Influence on priority**: Va justo después de vacantes: completa el primer “vertical slice” visible de extremo a extremo.

---

**US4 – Panel de candidatos por vacante con gestión de estados (pipeline básico)**

* **Impact**: Altísimo; aquí es donde el reclutador empieza a percibir el valor real del ATS: ver y organizar candidatos. Sin esto, solo somos un buzón de entrada de CVs.
* **Urgency**: Alta; es difícil vender o usar el producto sin permitir gestionar el pipeline (al menos unos pocos estados básicos). Es clave para mostrar que el producto no es solo un formulario de captación.
* **Complexity**: Media; listado, filtros sencillos y cambios de estado. Se puede empezar con algo muy simple y mejorar luego. No necesita IA ni sofisticación para ser útil.
* **Influence on priority**: Debe incluirse en el primer MVP, completando el ciclo “crear vacante → recibir candidatos → gestionar pipeline”.

---

**US5 – Ranking de candidatos con IA dentro del panel (scoring básico)**

* **Impact**: Alto porque es un factor diferencial frente a ATS tradicionales; ahorra tiempo de revisión y da una narrativa potente en ventas (“IA que prioriza candidatos”).
* **Urgency**: Media; el sistema ya es útil sin IA si el panel de candidatos es sólido. La IA es un “acelerador” y un diferenciador, no el cimiento.
* **Complexity**: Alta; introduce un módulo nuevo (IA), decisiones sobre features, latencias, explicabilidad y fallbacks. Hay riesgo de mala calidad percibida si el scoring no es razonable.
* **Influence on priority**: Muy adecuado para una segunda iteración después de estabilizar el flujo básico; no conviene que sea la primera gran pieza técnica.

---

**US6 – Programación automática de entrevistas con integración de calendario**

* **Impact**: Medio; mejora mucho la eficiencia, pero el problema puede resolverse inicialmente con correo y calendarios externos.
* **Urgency**: Media/Baja; los usuarios pueden trabajar sin esta función al principio. Es una muy buena mejora para un siguiente release.
* **Complexity**: Alta; integraciones externas, permisos, reprogramaciones, manejo de “no show”, etc. Muchas aristas no esenciales para un primer MVP.
* **Influence on priority**: Conviene posponerlo hasta que el flujo básico y el valor diferenciado (IA) estén consolidados.

---

**US7 – Multiposting de vacantes a portales de empleo externos**

* **Impact**: Medio/Alto; es muy valioso para agencias y empresas grandes, porque ahorra tiempo y centraliza postulaciones. Ayuda mucho al pitch comercial una vez que el core está firme.
* **Urgency**: Media; las empresas pueden inicialmente publicar manualmente en otros portales y usar LTI ATS como sistema central de gestión.
* **Complexity**: Alta; cada portal implica una integración diferente, formatos propios, gestión de errores y mantenibilidad a largo plazo.
* **Influence on priority**: También es una buena candidata para releases posteriores al MVP core; ofrece alto valor pero con complejidad y dependencia de terceros.

---

### Step 5: Ranked Prioritization List (Recommended Order)

**Resumen de la lógica de priorización**

1. Primero aseguramos un **núcleo funcional completo** y visible: reclutador entra, crea vacante, candidatos se postulan, el reclutador los ve y los mueve en un pipeline. Esto ofrece valor inmediato y es demostrable, sin depender de integraciones complejas ni IA madura.
2. Después, añadimos **diferenciadores de alto valor** (IA para ranking) que usan los datos generados por el núcleo y refuerzan la narrativa de producto innovador.
3. Finalmente, incorporamos **integraciones externas más complejas** (multiposting, calendario) que mejoran eficiencia y conveniencia, pero no son estrictamente necesarias para el uso inicial.

Con esa lógica:

1. **US1 – Recruiter login & secure access**
   (Habilita todo el trabajo interno y un espacio seguro de empresa.)

2. **US2 – Crear y gestionar vacantes (publicación en portal LTI, sin multiposting)**
   (Crea la pieza central del ATS y expone vacantes públicamente.)

3. **US3 – Portal de candidatos y postulación rápida con CV**
   (Completa el flujo extremo a extremo reclutador → candidato y empieza a generar datos.)

4. **US4 – Panel de candidatos por vacante con gestión de estados (pipeline básico)**
   (Da el valor práctico al reclutador: ver y gestionar candidatos; imprescindible en el MVP.)

5. **US5 – Ranking de candidatos con IA dentro del panel (scoring básico)**
   (Primera gran mejora diferencial: utiliza los datos ya existentes para aportar “inteligencia” y reducir carga manual.)

6. **US7 – Multiposting de vacantes a portales de empleo externos**
   (Optimiza la captación y añade valor para cuentas más avanzadas, una vez que el flujo interno está sólido.)

7. **US6 – Programación automática de entrevistas con integración de calendario**
   (Funcionalidad de eficiencia avanzada; recomendable para una fase posterior cuando el core y los diferenciales ya estén en producción.)

Este orden te da un **MVP funcional y demostrable** con las historias 1–4, un **MVP+ diferenciador** al añadir la 5, y un **camino claro de releases posteriores** con 6 y 7 para seguir aumentando valor sin bloquear el arranque del producto.

# Tickets de trabajo:
## Razonamiento (alto nivel)

Primero separo la **User Story “Crear y publicar vacante con multiposting”** en piezas de valor más pequeñas (sub user stories) que se puedan implementar y desplegar de forma incremental, respetando la priorización que ya definimos (primero núcleo de vacantes, luego multiposting):

### Sub user stories identificadas

1. **SU1 – Crear vacante en borrador**
   Como reclutador, quiero poder crear una vacante en estado borrador con los campos mínimos necesarios.
   👉 Esto implica: modelo de datos de vacante, endpoints de creación/edición, validaciones básicas y almacenamiento.

2. **SU2 – Publicar vacante en portal LTI (sin portales externos aún)**
   Como reclutador, quiero cambiar el estado de una vacante de “Borrador” a “Abierta” y que sea visible en el portal público de LTI.
   👉 Implica: lógica de cambio de estado, endpoint/listado público, URL pública y controles mínimos de visibilidad.

3. **SU3 – Gestionar ciclo de vida de la vacante (borrador/abierta/cerrada/archivada)**
   Como reclutador, quiero poder cerrar o archivar la vacante para que deje de recibir candidaturas.
   👉 Implica: estados adicionales, reglas de transición, actualizaciones de UI y API.

4. **SU4 – Configurar portales externos disponibles para multiposting**
   Como administrador de la empresa, quiero configurar qué portales externos están disponibles para publicar vacantes, sin que el reclutador tenga que ver credenciales.
   👉 Implica: modelo de configuración por empresa, almacenamiento de credenciales/config vía secretos, UI o al menos API interna.

5. **SU5 – Multipostear una vacante a portales externos desde la UI**
   Como reclutador, quiero seleccionar ciertos portales externos y publicar la vacante con un solo flujo de acción.
   👉 Implica: interfaz genérica de multiposting en backend, adaptadores para cada portal, endpoint que orquesta el envío, UI para seleccionar portales y disparar el multiposting.

6. **SU6 – Ver resultado del multiposting (éxito/error por portal)**
   Como reclutador, quiero ver si la publicación a cada portal fue exitosa o falló, para saber si debo actuar manualmente.
   👉 Implica: almacenamiento del resultado por portal, estructura de logs/resumen, exposición de ese estado en la UI.

7. **SU7 – Registrar canal de origen en las postulaciones (LTI vs portal externo)**
   Como reclutador, quiero saber de qué canal proviene cada candidatura (portal LTI, PortalExterno1, PortalExterno2…), para medir el rendimiento de cada fuente.
   👉 Implica: parámetro de origen en las URLs de multiposting, lectura de ese origen cuando el candidato se postula, campo “canalOrigen” en el modelo de Aplicación y visualización en el panel.

8. **SU8 – Auditoría y observabilidad básica de multiposting**
   Como equipo de producto/operaciones, quiero tener trazabilidad de los intentos de multiposting para poder diagnosticar errores y comportamientos extraños.
   👉 Implica: logging estructurado, quizás una tabla de “EventosMultiposting” y algunos filtros en backend/monitorización.

### Lógica de descomposición en tickets

A partir de estas sub user stories, distribuyo el trabajo en **tickets técnicos auto-contenidos**, intentando que:

* Cada ticket pueda ser entendido por sí mismo (desarrollador backend, frontend o devops).
* Se pueda avanzar por capas:

  * Primero modelo de datos y APIs de vacantes.
  * Luego UI interna del reclutador.
  * Después exposición pública de la vacante.
  * Finalmente la capa de multiposting, adaptadores, resultados y tracking de canal.
* Los tickets sean lo suficientemente específicos para que se pueda estimar y planificar:
  hay tickets de **back-end puro**, otros de **front-end**, otros de **integración** y de **infra/observabilidad**.

No incluyo aquí user stories de candidatos (postulación) ni panel de candidatos: solo cubro el alcance funcional relativo a **crear, publicar y multipostear vacantes**, y al **registro del origen de las postulaciones**, obligado por la propia user story.

---

## Lista de tickets

### Ticket 1: Modelo de datos de Vacante y estados básicos

* **Título:** Definir e implementar el modelo de datos de Vacante con estados básicos

* **Descripción detallada:**

  * **Propósito:**
    Definir la entidad `Vacante` en la base de datos y en el dominio de la aplicación, incluyendo los campos mínimos requeridos y los estados básicos de ciclo de vida (borrador, abierta, cerrada, archivada).
  * **Detalles específicos:**

    * Crear entidad/tabla `Vacante` con campos mínimos, por ejemplo (ajustable):

      * `id`
      * `empresaId`
      * `titulo`
      * `descripcion`
      * `ubicacion`
      * `tipoContrato`
      * `requisitosMinimos` (texto)
      * `salarioRango` [opcional]
      * `estado` (enum: BORRADOR, ABIERTA, CERRADA, ARCHIVADA)
      * `fechaCreacion`, `fechaActualizacion`
    * Definir enumeración de estados y regla general de validación (no lógica de transición aún).
    * Incluir índices básicos (por empresa, estado) para búsquedas eficientes.
    * Actualizar capa de modelo/dominio y repositorio/ORM.

* **Criterios de aceptación:**

  * La entidad `Vacante` existe en el código con los campos acordados.
  * La base de datos contiene la tabla/colección correspondiente, migración aplicada correctamente.
  * Se puede crear, leer y actualizar una instancia de `Vacante` desde la capa de repositorio en un test de integración.
  * Los estados permitidos están restringidos al enum definido.
  * Pruebas de validación de campos obligatorios a nivel de modelo (por ejemplo, título no nulo).

* **Prioridad:** Alta

* **Estimación de esfuerzo:** 3–5 puntos de historia

* **Asignación:** Equipo Backend / Ingeniero Backend

* **Etiquetas o tags:**

  * `feature:vacantes`
  * `type:backend`
  * `product:LTI-ATS`
  * `sprint:[Por definir]`

* **Comentarios y notas:**

  * Validar con Product qué campos son estrictamente obligatorios en la primera iteración.
  * Dejar espacio para extensiones futuras (por ejemplo, campos de categoría, seniority, remote/híbrido).

* **Enlaces o referencias:**

  * User Story: “Crear y publicar vacante con multiposting” [Por definir enlace al ticket padre]
  * PRD LTI ATS – Sección de Vacantes [Por definir]

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 2: Endpoints backend para CRUD básico de Vacantes (sin multiposting)

* **Título:** Implementar API REST para creación, edición, consulta y listado de vacantes

* **Descripción detallada:**

  * **Propósito:**
    Exponer servicios REST internos para que la UI del reclutador pueda crear, editar, obtener y listar vacantes, apoyándose en el modelo definido en el Ticket 1.
  * **Detalles específicos:**

    * Endpoints sugeridos (autenticados y con contexto de empresa):

      * `POST /api/vacantes` – crear vacante en estado BORRADOR.
      * `PUT /api/vacantes/{id}` – editar datos de la vacante (solo si no está cerrada/archivada).
      * `GET /api/vacantes/{id}` – obtener detalle de una vacante.
      * `GET /api/vacantes` – listar vacantes filtrando por empresa y opcionalmente por estado.
    * Validar que el `empresaId` del reclutador coincide con el de la vacante.
    * Manejo de errores: 404 si no existe, 403 si el usuario no tiene acceso, 400 para validaciones.
    * Tests de integración para cada endpoint.

* **Criterios de aceptación:**

  * Es posible crear una vacante en estado BORRADOR mediante `POST /api/vacantes`.
  * Es posible editar una vacante existente (excepto campos no permitidos o estados restringidos).
  * La lista de vacantes solo devuelve vacantes asociadas a la empresa del usuario autenticado.
  * Se devuelven códigos de estado HTTP adecuados (2xx, 4xx).
  * Existen pruebas automáticas que cubren los casos principales (crear, editar, listar, acceder a vacante inexistente).

* **Prioridad:** Alta

* **Estimación de esfuerzo:** 5 puntos de historia

* **Asignación:** Equipo Backend / Ingeniero Backend

* **Etiquetas o tags:**

  * `feature:vacantes`
  * `type:backend`
  * `type:api`
  * `product:LTI-ATS`
  * `sprint:[Por definir]`

* **Comentarios y notas:**

  * Alinear estructura de respuesta JSON con convenciones del resto del backend.
  * Incluir campos de paginación en el listado si se estima desde el comienzo.

* **Enlaces o referencias:**

  * Depende de: Ticket 1 – Modelo de datos de Vacante
  * User Story padre: “Crear y publicar vacante con multiposting” [Por definir]

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 3: Lógica de cambio de estado y publicación interna de vacantes

* **Título:** Implementar lógica de cambio de estado de vacante y endpoint de publicación en LTI

* **Descripción detallada:**

  * **Propósito:**
    Permitir que el reclutador cambie el estado de una vacante (por ejemplo, de BORRADOR a ABIERTA, de ABIERTA a CERRADA), y que la vacante esté marcada como “publicada internamente” cuando esté ABIERTA.
  * **Detalles específicos:**

    * Definir reglas de transición mínimas:

      * BORRADOR → ABIERTA
      * ABIERTA → CERRADA
      * CERRADA → ARCHIVADA
    * Implementar endpoint:

      * `POST /api/vacantes/{id}/publicar` – cambia de BORRADOR a ABIERTA (validando campos obligatorios llenos).
      * `POST /api/vacantes/{id}/cerrar` – cambia a CERRADA.
      * `POST /api/vacantes/{id}/archivar` – cambia a ARCHIVADA.
    * Validar que solo usuarios autorizados de la empresa puedan ejecutar estos cambios.
    * Manejar errores: no permitir transiciones inválidas (ej. ARCHIVADA → ABIERTA).

* **Criterios de aceptación:**

  * Se pueden ejecutar transiciones válidas de estado a través de los endpoints definidos.
  * Los intentos de transiciones inválidas devuelven error 400 con mensaje claro.
  * Una vacante en estado ABIERTA queda marcada como “visible” para el portal público LTI.
  * Existen pruebas unitarias y/o de integración que cubren transiciones válidas e inválidas.

* **Prioridad:** Alta

* **Estimación de esfuerzo:** 3–5 puntos de historia

* **Asignación:** Equipo Backend

* **Etiquetas o tags:**

  * `feature:vacantes`
  * `type:backend`
  * `type:business-rules`
  * `product:LTI-ATS`

* **Comentarios y notas:**

  * El comportamiento de “visible en portal público” se utilizará en el ticket de exposición pública de vacantes.

* **Enlaces o referencias:**

  * Ticket 1 – Modelo de datos de Vacante
  * Ticket 2 – Endpoints CRUD de Vacantes
  * User Story padre: “Crear y publicar vacante con multiposting”

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 4: UI interna – Formulario de creación y edición de vacante (reclutador)

* **Título:** Implementar formulario de creación y edición de vacante en la UI de reclutador

* **Descripción detallada:**

  * **Propósito:**
    Proveer una interfaz gráfica para que el reclutador pueda crear y editar vacantes, utilizando los endpoints backend existentes.
  * **Detalles específicos:**

    * Pantalla “Crear vacante”:

      * Campos mínimos: título, descripción, ubicación, tipo de contrato, requisitos mínimos.
      * Botones: “Guardar borrador”, “Cancelar”.
    * Pantalla “Editar vacante”:

      * Carga de datos existentes desde `/api/vacantes/{id}`.
      * Botones: “Guardar cambios”, “Volver”.
    * Validaciones en frontend (campos requeridos, longitud mínima, etc.).
    * Manejo de errores de API con mensajes amigables.

* **Criterios de aceptación:**

  * Un reclutador autenticado puede acceder a la pantalla de “Nueva vacante”, llenar el formulario y guardar un borrador exitosamente.
  * Un reclutador puede editar una vacante existente (en estados permitidos) y ver los cambios reflejados.
  * Los mensajes de error se muestran cuando faltan campos obligatorios o hay error de API.
  * La UI utiliza la API descrita en el Ticket 2 sin inconsistencias de formato.

* **Prioridad:** Alta

* **Estimación de esfuerzo:** 5 puntos de historia

* **Asignación:** Equipo Frontend / Ingeniero Frontend

* **Etiquetas o tags:**

  * `feature:vacantes`
  * `type:frontend`
  * `product:LTI-ATS`

* **Comentarios y notas:**

  * Utilizar componentes y diseño coherentes con el design system del producto.
  * Preparar el formulario para ser reutilizado en futuras ampliaciones de campos (sin acoplar demasiado la lógica).

* **Enlaces o referencias:**

  * Ticket 2 – API CRUD Vacantes
  * Ticket 3 – Lógica de estado (aunque aquí solo se necesita BORRADOR)
  * Mockups / wireframes: [Por definir]

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 5: UI interna – Listado de vacantes y acciones de publicación/cierre

* **Título:** Implementar listado de vacantes y acciones de publicación/cierre en la UI

* **Descripción detallada:**

  * **Propósito:**
    Permitir que el reclutador vea todas sus vacantes y ejecute acciones de cambio de estado (publicar, cerrar, archivar) desde una interfaz clara.
  * **Detalles específicos:**

    * Vista tipo tabla o tarjetas con: título, estado, fecha de creación, número de candidatos (placeholder), acciones.
    * Acciones por fila: “Editar”, “Publicar” (si BORRADOR), “Cerrar” (si ABIERTA), “Archivar” (si CERRADA).
    * Confirmaciones (modal) antes de cerrar/archivar.
    * Uso de endpoints del Ticket 3 para cambio de estado.

* **Criterios de aceptación:**

  * El reclutador ve un listado de sus vacantes, con estados claramente visibles.
  * Puede cambiar una vacante de BORRADOR a ABIERTA desde la UI y ver cómo el estado se actualiza.
  * Puede cerrar/archivar según reglas de negocio y ver los cambios reflejados.
  * Errores de API se manejan con mensajes claros.

* **Prioridad:** Alta

* **Estimación de esfuerzo:** 5 puntos de historia

* **Asignación:** Equipo Frontend

* **Etiquetas o tags:**

  * `feature:vacantes`
  * `type:frontend`
  * `product:LTI-ATS`

* **Comentarios y notas:**

  * Este listado será también el punto de entrada para el multiposting (tickets posteriores).

* **Enlaces o referencias:**

  * Ticket 2 – API CRUD Vacantes
  * Ticket 3 – Lógica de cambio de estado

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 6: Exposición pública de vacantes abiertas en el portal LTI

* **Título:** Implementar endpoint público y plantilla de detalle para vacantes abiertas

* **Descripción detallada:**

  * **Propósito:**
    Permitir que candidatos y visitantes externos vean las vacantes en estado ABIERTA en un portal público de LTI.
  * **Detalles específicos:**

    * Endpoint público de listado, por ejemplo: `GET /public/vacantes` (con filtros opcionales).
    * Endpoint de detalle: `GET /public/vacantes/{slug-o-id}`.
    * Plantilla básica de detalle de vacante (título, descripción, ubicación, tipo de contrato, etc.).
    * Solo mostrar vacantes con estado ABIERTA.

* **Criterios de aceptación:**

  * Un usuario no autenticado puede acceder al listado de vacantes abiertas y ver información básica.
  * Un usuario no autenticado puede ver la página de detalle de una vacante ABIERTA.
  * Vacantes en otros estados no son visibles a través de estos endpoints.
  * Se garantiza que no se exponen datos sensibles adicionales (ej. información interna de empresa).

* **Prioridad:** Alta

* **Estimación de esfuerzo:** 5 puntos de historia

* **Asignación:** Equipo Backend + Frontend (si la plantilla se renderiza en web app)

* **Etiquetas o tags:**

  * `feature:vacantes`
  * `feature:portal-publico`
  * `type:backend`
  * `type:frontend`

* **Comentarios y notas:**

  * Esta página pública será también el punto de entrada para la postulación (otra user story).

* **Enlaces o referencias:**

  * Ticket 3 – Lógica de cambio de estado (ABIERTA)
  * Diseños de portal de vacantes: [Por definir]

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 7: Modelo de configuración de portales externos para multiposting

* **Título:** Definir modelo de datos y almacenamiento de configuración de portales externos de empleo

* **Descripción detallada:**

  * **Propósito:**
    Permitir almacenar, a nivel de empresa, qué portales externos de empleo están configurados para multiposting y con qué parámetros (API keys, URLs base, etc.).
  * **Detalles específicos:**

    * Entidad/tabla `PortalExterno` (catálogo general) con campos:

      * `id`, `nombre`, `tipo`, `urlBaseApi`, `documentacionReferencia` [opcional].
    * Entidad/tabla `ConfiguracionPortalEmpresa` con campos:

      * `id`, `empresaId`, `portalExternoId`, `credenciales` (enlace a secreto o estructura encriptada), `activo`.
    * Considerar integración con gestor de secretos para credenciales.
    * Repositorios y métodos de acceso para recuperar la lista de portales activos por empresa.

* **Criterios de aceptación:**

  * Existe un modelo de datos capaz de representar portales externos y su configuración por empresa.
  * Se puede registrar al menos un portal externo (ej. “PortalExterno1”) y marcarlo como activo para una empresa específica.
  * El backend puede recuperar la lista de portales activos para una empresa sin exponer credenciales en claro.

* **Prioridad:** Media-Alta

* **Estimación de esfuerzo:** 3–5 puntos de historia

* **Asignación:** Equipo Backend / DevOps (para tema de secretos)

* **Etiquetas o tags:**

  * `feature:multiposting`
  * `type:backend`
  * `type:infra`

* **Comentarios y notas:**

  * No es obligatorio tener UI de gestión en esta primera iteración; puede configurarse vía scripts/admin.

* **Enlaces o referencias:**

  * User Story padre: “Crear y publicar vacante con multiposting”
  * Ticket 1 – Vacante (para `empresaId`)

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 8: Interfaz genérica de multiposting y adaptador para PortalExterno1

* **Título:** Implementar servicio de multiposting y adaptador de integración para PortalExterno1

* **Descripción detallada:**

  * **Propósito:**
    Desarrollar una interfaz genérica de multiposting en el backend y un primer adaptador concreto para un portal externo (`PortalExterno1`), capaz de recibir una vacante y publicarla.
  * **Detalles específicos:**

    * Definir interfaz `MultipostingProvider` con métodos, por ejemplo:

      * `publicarVacante(vacante, configPortalEmpresa): ResultadoPublicacion`.
    * Implementar clase `PortalExterno1Provider` que cumpla la interfaz y se conecte a una API ejemplar (especificación simulada/local).
    * Implementar servicio `MultipostingService` que:

      * Obtenga configuración de portales activos (Ticket 7).
      * Llame al proveedor correspondiente por portal.
      * Devuelva un resultado por portal (éxito/error, mensaje).
    * Manejo de timeouts y reintentos sencillos.

* **Criterios de aceptación:**

  * Desde código, es posible invocar `MultipostingService` con una vacante y una empresa, y obtener resultados por portal (al menos PortalExterno1).
  * El adaptador de PortalExterno1 maneja correctamente casos de éxito y error simulados (tests).
  * Se ejecutan pruebas unitarias para el servicio de multiposting y el adaptador.

* **Prioridad:** Media-Alta

* **Estimación de esfuerzo:** 8 puntos de historia

* **Asignación:** Equipo Backend

* **Etiquetas o tags:**

  * `feature:multiposting`
  * `type:backend`
  * `type:integration`

* **Comentarios y notas:**

  * La implementación puede inicialmente consumir un “mock server” para PortalExterno1 hasta que exista una API real.

* **Enlaces o referencias:**

  * Ticket 7 – Configuración de portales externos
  * Especificación técnica API PortalExterno1: [Por definir]

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 9: Endpoint backend para disparar multiposting desde una vacante

* **Título:** Implementar endpoint REST para ejecutar multiposting de una vacante

* **Descripción detallada:**

  * **Propósito:**
    Permitir que la UI del reclutador dispare el multiposting de una vacante específica hacia uno o varios portales configurados.
  * **Detalles específicos:**

    * Endpoint autenticado, por ejemplo:

      * `POST /api/vacantes/{id}/multiposting`

        * Body: lista de `portalExternoId` seleccionados.
    * Validaciones:

      * La vacante debe estar en estado ABIERTA.
      * La vacante debe pertenecer a la empresa del usuario.
      * Los portales seleccionados deben estar configurados y activos para esa empresa.
    * Integración con `MultipostingService` (Ticket 8).
    * Estructura de respuesta: resultados por portal (éxito/error, mensaje, timestamp).
    * Registro de intento/resultados en entidad de auditoría (Ticket 11/12).

* **Criterios de aceptación:**

  * Un llamado válido al endpoint ejecuta multiposting en los portales seleccionados y devuelve el resultado por portal.
  * Un llamado con vacante no ABIERTA devuelve error apropiado (400 o 409).
  * Un llamado con portal no configurado devuelve error claro (400).
  * Existen pruebas de integración que verifican la orquestación completa.

* **Prioridad:** Media-Alta

* **Estimación de esfuerzo:** 5 puntos de historia

* **Asignación:** Equipo Backend

* **Etiquetas o tags:**

  * `feature:multiposting`
  * `feature:vacantes`
  * `type:backend`
  * `type:api`

* **Comentarios y notas:**

  * Dejamos la ejecución como síncrona en esta primera versión; si el tiempo de respuesta es elevado, se puede refactorizar a colas/jobs.

* **Enlaces o referencias:**

  * Ticket 3 – Lógica de estado de vacante
  * Ticket 7 – Configuración portales
  * Ticket 8 – Servicio de multiposting

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 10: UI interna – Selección de portales y visualización de resultado de multiposting

* **Título:** Añadir en la UI de vacantes la selección de portales y feedback de multiposting

* **Descripción detallada:**

  * **Propósito:**
    Permitir que el reclutador, desde la pantalla de detalle o listado de vacante, seleccione portales externos para multiposting y vea el resultado inmediato por portal.
  * **Detalles específicos:**

    * En detalle de vacante en estado ABIERTA, añadir sección “Publicar en portales externos”:

      * Lista de portales activos para la empresa (obtenida desde un endpoint, o embebida en la respuesta de la vacante).
      * Checkbox o select para elegir uno o varios portales.
      * Botón “Publicar en portales seleccionados”.
    * Tras ejecutar la acción:

      * Mostrar resultado por portal (éxito/error, mensaje).
      * Opcional: persistir la última fecha/estado de publicación y mostrarlo.

* **Criterios de aceptación:**

  * Un reclutador ve qué portales externos tiene disponibles para multiposting.
  * Puede seleccionar uno o varios portales y disparar multiposting; la UI muestra feedback por portal.
  * Si el endpoint devuelve error global o parcial, la UI informa claramente qué pasó.

* **Prioridad:** Media

* **Estimación de esfuerzo:** 5 puntos de historia

* **Asignación:** Equipo Frontend

* **Etiquetas o tags:**

  * `feature:multiposting`
  * `feature:vacantes`
  * `type:frontend`

* **Comentarios y notas:**

  * Diseñar la sección pensando en que en el futuro puede haber 5–10 portales activos.

* **Enlaces o referencias:**

  * Ticket 7 – Modelo de portales externos
  * Ticket 9 – Endpoint de multiposting

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 11: Modelo de auditoría de multiposting y logging estructurado

* **Título:** Implementar auditoría de multiposting y logging estructurado por portal

* **Descripción detallada:**

  * **Propósito:**
    Registrar cada intento de multiposting y sus resultados para poder consultarlos y diagnosticar problemas.
  * **Detalles específicos:**

    * Entidad/tabla `EventoMultiposting` con campos:

      * `id`, `vacanteId`, `empresaId`, `portalExternoId`, `estado` (EXITO/ERROR), `mensaje`, `fechaEvento`, `payloadResumen` [opcional].
    * En `MultipostingService` y/o en el endpoint, guardar un `EventoMultiposting` por portal.
    * Logging estructurado (en logs de aplicación) alineado con la información de la entidad.

* **Criterios de aceptación:**

  * Cada ejecución de multiposting genera uno o más registros de `EventoMultiposting`.
  * En los logs de la aplicación se puede filtrar por `vacanteId` o `portalExternoId` y ver el histórico de intentos.
  * Se pueden consultar los eventos desde la capa de datos (aunque inicialmente no haya UI).

* **Prioridad:** Media

* **Estimación de esfuerzo:** 3–5 puntos de historia

* **Asignación:** Equipo Backend / DevOps

* **Etiquetas o tags:**

  * `feature:multiposting`
  * `type:backend`
  * `type:observability`

* **Comentarios y notas:**

  * En un futuro se puede construir una UI de “historial de publicación” sobre esta entidad.

* **Enlaces o referencias:**

  * Ticket 8 – MultipostingService
  * Ticket 9 – Endpoint multiposting

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 12: Extensión del modelo de Aplicación/Candidatura con canal de origen

* **Título:** Añadir campo “canalOrigen” a la entidad de Aplicación/Candidatura

* **Descripción detallada:**

  * **Propósito:**
    Permitir identificar el canal de origen de cada candidatura (portal LTI, PortalExterno1, PortalExterno2…).
  * **Detalles específicos:**

    * Extender entidad/tabla `Aplicacion` (o equivalente) con campo `canalOrigen` (string o enum).
    * Valores posibles iniciales:

      * `LTI_PORTAL`
      * `PORTAL_EXTERNO_1`
      * `PORTAL_EXTERNO_2`
    * Migraciones necesarias.

* **Criterios de aceptación:**

  * El modelo de datos de Aplicación incluye el campo `canalOrigen`.
  * Se pueden crear registros de Aplicación especificando un valor de `canalOrigen`.
  * Las migraciones no rompen datos existentes (si los hay).

* **Prioridad:** Media

* **Estimación de esfuerzo:** 3 puntos de historia

* **Asignación:** Equipo Backend

* **Etiquetas o tags:**

  * `feature:multiposting`
  * `feature:analytics`
  * `type:backend`

* **Comentarios y notas:**

  * La visualización del canal en el panel de candidatos se definirá en otra user story, pero la base de datos debe estar lista.

* **Enlaces o referencias:**

  * User Story padre
  * Modelo de Aplicación actual: [Por definir]

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

### Ticket 13: Gestión del canal de origen en URLs de publicación y flujo de postulación

* **Título:** Implementar mecanismos para propagar canal de origen desde los portales externos hasta la candidatura

* **Descripción detallada:**

  * **Propósito:**
    Garantizar que cuando un candidato llega desde un portal externo y se postula, el sistema registre correctamente el `canalOrigen` en la Aplicación.
  * **Detalles específicos:**

    * Definir convención de `utm` o parámetros de query en la URL de la vacante, por ejemplo:

      * `?source=PORTAL_EXTERNO_1`
    * Asegurar que los adaptadores de multiposting generan URLs de vacante incluyendo el parámetro correcto para cada portal.
    * En el flujo de postulación (endpoint de creación de Aplicación), leer dicho parámetro y asignarlo al campo `canalOrigen` (Ticket 12).
    * Definir valor por defecto `LTI_PORTAL` cuando no exista parámetro de origen.

* **Criterios de aceptación:**

  * Si un candidato entra a la página de vacante con `?source=PORTAL_EXTERNO_1` y se postula, la Aplicación creada tiene `canalOrigen=PORTAL_EXTERNO_1`.
  * Si entra sin parámetro de source (ej. acceso directo al portal LTI), la Aplicación se crea con `canalOrigen=LTI_PORTAL`.
  * Los enlaces generados por multiposting incluyen el parámetro de `source` adecuado.

* **Prioridad:** Media

* **Estimación de esfuerzo:** 5 puntos de historia

* **Asignación:** Backend (para flujo de postulación) + posiblemente Frontend portal público

* **Etiquetas o tags:**

  * `feature:multiposting`
  * `feature:analytics`
  * `type:backend`
  * `type:frontend`

* **Comentarios y notas:**

  * Coordinar con la user story de postulación de candidatos para asegurar que el endpoint y la UI respetan estos parámetros.

* **Enlaces o referencias:**

  * Ticket 8 – MultipostingService (para URLs generadas).
  * Ticket 12 – Campo canalOrigen.
  * User story de postulación de candidatos: [Por definir].

* **Historial de cambios:**

  * [Por definir] – Creación inicial del ticket.

---

Con estos tickets, el alcance de la User Story “Crear y publicar vacante con multiposting” queda cubierto extremo a extremo: desde el modelo de vacante y su publicación interna, hasta la **configuración y ejecución del multiposting**, auditoría de resultados y **tracking del canal de origen** de las candidaturas.
