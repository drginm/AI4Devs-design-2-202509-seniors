# Prompt 1: Generate User Stories

actuar como un Product Manager y Business Analyst experto para una startup llamada LTI que está desarrollando un sistema de seguimiento de candidatos (ATS) innovador. tu tarea es dado un PRD con la definicion del producto attached en este mensaje, generar los siguientes artefactos de diseño de software:

Generar las User Stories. Puedes implementar tantas como quieras y puedas, el mínimo son 2. Utiliza lo aprendido sobre buenas prácticas de este capítulo para que contenga toda la información necesaria, y como consejo, usa una plantilla común para todas ellas (recuerda que dejamos un ejemplo de plantilla en la sección de User Stories).

Usa mejores practicas para escribir user stories: 

#### Características de las User Stories

Las User Stories describen una característica del software desde la perspectiva del usuario final. 

Las características más importantes que deben cumplir las User Stories para cumplir su cometido son:

1. **Descripción informal y en lenguaje natural**: Las User Stories describen las características del software de una manera sencilla y no técnica, desde el punto de vista del usuario. Es importante el storytelling, no es una descripción técnica, y si se puede vincular al avatar / buyer persona / usuario que lo demanda, mejor.
2. **Enfocadas en el usuario**: Las User Stories se enfocan en lo que el usuario quiere lograr, en lugar de en las funcionalidades técnicas del sistema.
3. **Estructura clásica**: Generalmente siguen el formato: "Como un [tipo de usuario], quiero [realizar una acción] para [obtener un beneficio]".
4. Incluir criterios de aceptación:
    - Definir claramente los criterios que deben cumplirse para considerar una historia "terminada".
    - Evitar centrarse en cómo se construirá la funcionalidad.
    - Gherkin format

  Scenario: Successful login with valid credentials
    Given the user is on the login page
    When the user enters a valid username and password
    And clicks the "Login" button
    Then the user should be redirected to their dashboard
    And a welcome message should be displayed

1. **Priorización y estimación**: Las User Stories se priorizan, y se les asigna un esfuerzo estimado por parte del equipo de desarrollo en caso de que sea una de las variables a tener en cuenta en la priorización.
2. **Conversación y confirmación**: Las User Stories fomentan la conversación entre los responsables de producto, los stakeholders y el equipo técnico, y se confirman una vez que la funcionalidad se ha implementado.
3. **Evolución iterativa**: A medida que el proyecto avanza, las User Stories pueden evolucionar y cambiar para adaptarse a las necesidades cambiantes.

#### Estructura basica de una User Story

1. **Formato estándar**: "Como [tipo de usuario], quiero [realizar una acción] para [obtener un beneficio]".
2. **Descripción**: Una descripción concisa y en lenguaje natural de la funcionalidad que el usuario desea.
3. **Criterios de Aceptación**: Condiciones específicas que deben cumplirse para considerar la User Story como "terminada", éstos deberian de seguir un formato similar a “Dado que” [contexto inicial], "cuando” [acción realizada], “entonces” [resultado esperado].
4. Notas adicionales:  Notas que puedan ayudar al desarrollo de la historia
5. Tareas: Lista de tareas y subtareas para que esta historia pueda ser completada

## Response

Actúa como un Product Manager y Business Analyst experto para una startup llamada LTI que desarrolla un sistema innovador de seguimiento de candidatos (ATS). Dados los requerimientos del PRD proporcionados, tu tarea es generar User Stories siguiendo las mejores prácticas: deben estar escritas en lenguaje natural, centradas en el usuario, contar con criterios de aceptación en formato Gherkin, priorización y estimación, y una estructura homogénea; incluye mínimo 2 User Stories. Asegúrate de completar cada sección de la plantilla detallada, priorizar las historias y asignar esfuerzo estimado. Usa storytelling y vincula las historias al perfil del usuario o buyer persona relevante cuando sea posible.

Sigue la siguiente plantilla para cada User Story:

1. **Título**: Breve y descriptivo.
2. **Formato estándar**: "Como [tipo de usuario], quiero [realizar una acción] para [obtener un beneficio]".
3. **Descripción**: Explica en lenguaje sencillo el valor/beneficio.
4. **Criterios de aceptación** (en formato Gherkin: Dado que/Cuando/Entonces).
5. **Priorización**: Indica el nivel (Ej. Alta, Media, Baja).
6. **Esfuerzo estimado**: Número de puntos o t-shirt size (S, M, L, XL).
7. **Notas adicionales**: Consideraciones relevantes para entender el contexto o restricciones.
8. **Tareas**: Lista paso a paso de tareas y subtareas para la implementación.

Persiste hasta que todas las secciones estén completas para cada User Story antes de finalizar tu respuesta. Utiliza un razonamiento explícito y paso a paso antes de definir cada User Story y sus elementos. No inicies ninguna User Story con conclusiones; primero, analiza el flujo del usuario y sus necesidades, luego redacta la historia con el formato adecuado.

## Formato de salida requerido
- Presenta cada User Story completa en formato markdown siguiendo el orden y estructura indicada arriba.
- Usa títulos y subtítulos para separar cada historia.
- Utiliza listas numeradas, viñetas y tablas si es necesario para claridad.
- Incluye al menos 2 User Stories, pero agrega más si lo consideras valioso para cubrir los requisitos del PRD.
- La longitud y detalle de cada User Story debe ser suficiente para que cualquier desarrollador comprenda el requerimiento y pueda discutirlo.

## Ejemplo de User Story COMPLETA (usa siempre la plantilla propuesta):
### User Story 1: Acceso de Reclutador a Panel de Candidatos

- **Como** reclutador,
- **quiero** ver una lista de todos los candidatos aplicados a una vacante,
- **para** poder gestionar eficientemente el proceso de selección.

**Descripción**: Permite a los reclutadores visualizar, filtrar y acceder a información relevante de candidatos desde un único panel centralizado.

**Criterios de aceptación**:
- **Scenario 1: Visualización de candidatos aplicados**
    - Dado que soy un reclutador y he iniciado sesión,
    - cuando accedo al panel de una vacante,
    - entonces debería ver una lista de candidatos aplicados a esa vacante con datos básicos (nombre, fecha de aplicación, estatus).
- **Scenario 2: Filtros en la lista**
    - Dado que estoy viendo la lista de candidatos,
    - cuando aplico filtros por estatus o fecha,
    - entonces la lista debe reflejar solo los candidatos que cumplen esos criterios.

**Priorización**: Alta  
**Esfuerzo estimado**: M  
**Notas adicionales**: Los datos deben cargarse rápidamente para no afectar la experiencia de usuario.  
**Tareas**:
- Configurar endpoint backend para obtener candidatos por vacante
- Implementar UI para visualizar lista de candidatos y filtros
- Validar con usuarios clave el diseño preliminar

---

(Este ejemplo debe adaptarse a la longitud real y a las funcionalidades cubiertas en el PRD. Para historias más complejas, expande los criterios de aceptación y tareas usando [PLACEHOLDERS] o descripciones detalladas según lo requerido.)

---

**Recordatorio esencial:**  
- Sigue la plantilla y las mejores prácticas detalladas.
- Inicia con razonamiento/flujo, termina con la User Story.
- Mantén el enfoque en claridad, completitud y utilidad para equipos de desarrollo/producto.

# Prompt 2: Backlog priorizado

actuar como un Product Manager y Business Analyst experto para una startup llamada LTI que está desarrollando un sistema de seguimiento de candidatos (ATS) innovador., tu tarea es definir una estrategia de priorizacion, actualmente no se cuenta con ningun historico , para priorizar debemos empezar por tasks importantes pero q a su vez puedan ir mostrando partes de la aplicacion sin iniciar por la mas compleja, debe haber un balance entre complejidad, valor para el negocio dado q la aplicacion se creara desde cero #### **Factores para la Priorización del Backlog**  1. **Valor del Negocio:** Identificar las user stories y mejoras que aportan el mayor valor al negocio o a los usuarios finales. Esto incluye impacto en la retención de usuarios, atractivo para nuevos usuarios y potencial de ingresos. 2. **Urgencia:** Determinar qué características son más urgentes en términos de necesidades del mercado o compromisos con los stakeholders. 3. **Dependencias:** Reconocer y priorizar tareas que otras tareas dependen para su implementación. Esto asegura un flujo de trabajo lógico y eficiente. 4. **Coste de implementación:** Considerar el esfuerzo, los recursos y el tiempo necesarios para cada tarea. Priorizar aquellas con la mejor relación costo-beneficio. 5. **Riesgos y obstáculos potenciales:** Evaluar los riesgos asociados con cada user story o mejora y su impacto potencial en el proyecto. 6. **Feedback del usuario:** Integrar las opiniones y preferencias de los usuarios, especialmente en áreas críticas de la interfaz de usuario y la experiencia del usuario. 7. **Madurez tecnológica:** Considerar la madurez y la viabilidad de las soluciones tecnológicas propuestas para cada tarea.
la informacion debe sacarse del chat actual, debe generarse una table con las use stories
> Estima por cada item en el backlog (genera una tabla markdown):
> 
> - Impacto en el usuario y valor del negocio.
> - Urgencia basada en tendencias del mercado y feedback de usuarios.
> - Complejidad y esfuerzo estimado de implementación.
> - Riesgos y dependencias entre tareas.

## Response

You are acting as a Product Manager and Business Analyst expert for a startup called LTI, which is building an innovative applicant tracking system (ATS) from scratch. Your objective is to define an actionable and logical prioritization strategy for the initial product backlog, given the absence of prior historical data. Focus on tasks that provide high business/user value and can showcase functional parts of the product early—do not begin with the most complex features. Achieve a balance between implementation complexity, business value, and stepwise product visibility.

### Guidelines for the Prioritization Strategy

- **Step 1: Identify and List Key User Stories**
  - Infer and draft initial user stories suitable for an MVP from the current chat context and requirement.
- **Step 2: Analyze Each User Story Against Prioritization Factors**
  For each story, estimate:
  - Impact on the user and business value
  - Urgency (market trends, user feedback, stakeholder commitments)
  - Implementation complexity/effort (qualitative estimate)
  - Risks and dependencies (technical, sequence, learning curve)
- **Step 3: Organize Results in a Clear Markdown Table**
  - Each row = One user story/backlog item.
  - Columns: User Story | Business/User Impact | Urgency | Implementation Complexity | Risks & Dependencies
- **Step 4: Reason Before Concluding Prioritization**
  - For each story, show brief reasoning for each factor before stating how it influences priority.
- **Step 5: Recommend Ranking Order**
  - Based only on the reasoning above (rank or flag likely candidates for MVP/highest value).
- Only base information on the current chat context; do not assume external data.

### Output Format

- Your output should be a markdown-formatted response.
- Display one unified table, with columns labeled:
  - User Story
  - Business/User Impact (High/Med/Low + reason)
  - Urgency (High/Med/Low + reason)
  - Implementation Complexity (High/Med/Low + reason)
  - Risks & Dependencies (Bullet points)
- Below the table, provide a ranked list (1. …, 2. …, etc.) of the user stories for development, based on the matrix analysis.
- Before the ranked list, briefly summarize your reasoning chain (do NOT state conclusions before your reasoning).

---

### Example

#### Step 1-3: User Stories Table

| User Story                            | Business/User Impact            | Urgency             | Implementation Complexity    | Risks & Dependencies                      |
|----------------------------------------|---------------------------------|---------------------|-----------------------------|-------------------------------------------|
| [Placeholder user story: e.g. Login]   | High – Enables access control   | High – Core entry   | Low – Standard implementation| None                                       |
| [Placeholder: Candidate profile]       | Med – Needed to store data      | Med – Early needed  | Med – Some DB design         | Depends on login system                   |
| ...                                    | ...                             | ...                 | ...                         | ...                                       |

#### Step 4: Reasoning

- Feature A (e.g., Login): Critical for secure user entry and system access, little risk, quick win.
- Feature B (e.g., Candidate Profile): Necessary for the ATS to function, but depends on authentication.
- Feature C: [Etc.]

#### Step 5: Ranked Prioritization List

1. [Login]
2. [Candidate Profile]
3. [...]

---

**Important: For each user story/backlog item, ensure that you explain your justification for each estimate before ranking. Only produce conclusions (ranking/list) AFTER the justification. Do NOT use code blocks for the table.**

---

**REMINDER:**
- Prioritize tasks that display early product value without excessive complexity.
- Apply and justify each prioritization factor per guidelines and table columns.
- Base your analysis ONLY on the current chat context, not assumed data.



Generar las User Stories. Puedes implementar tantas como quieras y puedas, el mínimo son 2. Utiliza lo aprendido sobre buenas prácticas de este capítulo para que contenga toda la información necesaria, y como consejo, usa una plantilla común para todas ellas (recuerda que dejamos un ejemplo de plantilla en la sección de User Stories).
Arma el Backlog de producto con las User Stories, priorizándolas como consideres conveniente acorde a alguna metodología concreta. experimenta con diferentes formas de generar un prompt que te pueda genera tu back log basado en la documentación que has generado previamente. Entrega los diferentes prompts que usaste e indica cual prompt te dio mejores resultados. Entrega junto a los prompts tus conclusiones, por qué crees este prompt fue efectivo. 
Elige la User Story que prefieras, y genera los Tickets de trabajo. Aterrízalos técnicamente, tal y como se hace en las reuniones de planificación
(Extra 🎁) Estima el esfuerzo de los tickets de trabajo usando la metodología (fibonacci, poker, tallas de camiseta) y unidades (horas, puntos de historia) que prefieras.

## Rationale

No use otro prompt pues la respuesta de este fue muy acorde a lo q habria esperado, de hecho partio las US originales en mas pequeñas y detalladas, lo cual es ideal para un backlog inicial.

# Tickets de trabajo para la User Story:

actuar como un Product Manager y Business Analyst experto para una startup llamada LTI que está desarrollando un sistema de seguimiento de candidatos (ATS) innovador. Tu tarea es desglosar la User Story "User Story 1: Crear y publicar vacante con multiposting" en tickets de trabajo técnicos detallados, adecuados para la planificación de sprints de desarrollo, tomando en cuenta las sub user stories q creaste al priorizar el backlog. la salida debe ser una lista de tickets de trabajo en markdown toma en cuenta las mejores practicas para crear un ticket de trabajo: Un ticket de trabajo efectivo debe contener toda la información necesaria para que cualquier miembro del equipo comprenda y ejecute la tarea adecuadamente. Aquí se enumeran los elementos más importantes que debería incluir un ticket de trabajo para maximizar su claridad y eficacia:  **1. Título Claro y Conciso**  Un resumen breve que refleje la esencia de la tarea. Debe ser lo suficientemente descriptivo para que cualquier miembro del equipo entienda rápidamente de qué se trata el ticket.  **2. Descripción Detallada**  - **Propósito:** Explicación de por qué es necesaria la tarea y qué problema resuelve. - **Detalles Específicos:** Información adicional sobre requerimientos específicos, restricciones, o condiciones necesarias para la realización de la tarea.  **3. Criterios de Aceptación**  - **Expectativas Claras:** Lista detallada de condiciones que deben cumplirse para que el trabajo en el ticket se considere completado. - **Pruebas de Validación:** Pasos o pruebas específicas que se deben realizar para verificar que la tarea se ha completado correctamente.  **4. Prioridad**  - **Nivel de Urgencia:** Una clasificación de la importancia y la urgencia de la tarea, lo cual ayuda a determinar el orden en que deben ser abordadas las tareas dentro del backlog.  **5. Estimación de Esfuerzo**  - **Puntos de Historia o Tiempo Estimado:** Una evaluación del tiempo o esfuerzo que se espera que tome completar el ticket. Esto es esencial para la planificación y gestión del tiempo del equipo.  **6. Asignación**  - **Responsable:** Quién o qué equipo será responsable de completar la tarea. Esto asegura que todos los involucrados entiendan quién está a cargo de cada parte del proyecto.  **7. Etiquetas o Tags**  - **Categorización:** Etiquetas que ayudan a clasificar el ticket por tipo (bug, mejora, tarea, etc.), por características del producto (UI, backend, etc.), o por sprint/versión.  **8. Comentarios y Notas**  - **Colaboración:** Espacio para que los miembros del equipo agreguen información relevante, hagan preguntas, o proporcionen actualizaciones sobre el progreso de la tarea.  **9. Enlaces o Referencias**  - **Documentación Relacionada:** Enlaces a documentos, diseños, especificaciones o tickets relacionados que proporcionen contexto adicional o información necesaria para la ejecución de la tarea.  **10. Historial de Cambios**  - **Rastreo de Modificaciones:** Un registro de todos los cambios realizados en el ticket, incluyendo actualizaciones de estado, reasignaciones y modificaciones en los detalles o prioridades.

## Response

Desglosa la User Story "User Story 1: Crear y publicar vacante con multiposting" en tickets de trabajo técnicos detallados y auto-contenidos, cada uno siguiendo las mejores prácticas especificadas. La salida debe ser una lista en formato markdown donde cada ticket incluye los siguientes elementos:

- **Título claro y conciso**  
- **Descripción detallada**  
  - Propósito  
  - Detalles específicos  
- **Criterios de aceptación**  
  - Expectativas claras  
  - Pruebas de validación  
- **Prioridad** (ej. Alta / Media / Baja)  
- **Estimación de esfuerzo** (en puntos de historia o tiempo estimado)  
- **Asignación** (rol o equipo sugerido responsable)  
- **Etiquetas o tags** (tipo de tarea, característica, producto, sprint)  
- **Comentarios y notas** (espacio para aclaraciones o comunicación de avances y dudas)  
- **Enlaces o referencias** (a documentos, especificaciones, tickets relacionados)  
- **Historial de cambios** (registro de actualizaciones sobre el ticket)

Antes de dividir en tickets, identifica razonadamente las sub user stories relacionadas a la funcionalidad de "Crear y publicar vacante con multiposting", basándote en la priorización del backlog que tú mismo generaste, y usa estas sub user stories como guía para el desglose de tickets.

**Razona explícitamente antes de crear cualquier ticket; describe cómo chaque sub user story se traduce en tareas técnicas y la lógica de su descomposición. Solo tras este razonamiento produce la lista detallada de tickets.** Asegúrate de persistir hasta que el desglose cubra todo el alcance funcional (no dejes aspectos relevantes sin ticket). Utiliza el encadenamiento de ideas interno ("chain of thought") antes de listar tu respuesta final: primero argumenta y planifica tu enfoque, luego presenta los tickets.

**Formato de salida:**  
- Una sección de reasoning o razonamiento detallado antes de la lista de tickets, donde expliques brevemente la lógica y los pasos de tu descomposición.  
- Un listado de tickets en formato markdown, con cada uno siguiendo rigurosamente los 10 elementos descritos.  
- Si algún campo no se puede llenar por contexto insuficiente, deja el placeholder [Por definir].  
- Cada ticket debe ser lo suficientemente detallado como para ser entendido y ejecutado por cualquier miembro del equipo técnico.

# Ejemplo de estructura de salida (usa ejemplos más complejos y completos en el output real):

## Razonamiento
[Ejemplo:]  
Para "Crear y publicar vacante con multiposting", identifico las siguientes sub user stories:  
- Como reclutador, quiero poder ingresar los detalles de una vacante.  
- Como reclutador, quiero publicar la vacante en múltiples portales automáticamente.  
- Como usuario, quiero visualizar el historial de publicación.  
Estas se traducen en tareas como: diseño de formulario, integración con APIs externas, registro de logs, y validaciones.

## Lista de tickets

### Ticket 1: Diseño e implementación del formulario de creación de vacante

- **Título:** [Ejemplo: Implementar formulario para creación de vacante]
- **Descripción:** [...]  
...
- **Historial de cambios:** [...]

### Ticket 2: ...
(y así sucesivamente)

*(En ejemplos reales, utiliza datos y requerimientos propios de la funcionalidad de multiposting en un ATS, con descripciones y criterios de aceptación extendidos y detallados, y todos los campos completos o con placeholder si algún dato falta.)*

# Importante  
- El razonamiento argumentativo va siempre ANTES de los tickets.  
- Concluye SOLO después de toda la lista de tickets.  
- No omitas ningún campo de los 10 especificados por ticket.  
- La salida es en MARKDOWN, NO en bloque de código.

# Recordatorio:  
Desglosa la User Story "Crear y publicar vacante con multiposting" en tickets técnicos exhaustivos, argumenta y planifica primero, luego produce la lista detallada, cada ticket incluyendo los 10 elementos especificados.

