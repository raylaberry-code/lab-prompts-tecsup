# Biblioteca de prompts - Laboratorio 06

Alumno: Ray Laberry Cherre | Curso: Diseño de Interfaces de Programación Avanzado | Sección: C24

---

## Prueba 1 - Prompt vago

**Herramienta:** Claude

**Prompt:**

> Escribe un correo pidiendo más plazo para un trabajo.

**Resultado (resumen):** Claude entregó una plantilla de correo con dos versiones (para profesor/a y para jefe/a o cliente), con muchos datos entre corchetes por completar y un motivo genérico con varias opciones.

**Observaciones:** El prompt no decía quién escribía, a quién ni por qué, así que el modelo tuvo que adivinar. Por eso ofreció dos destinatarios posibles, dejó la fecha y el motivo sin definir y terminó pidiendo más detalles para ajustar el correo.

---

## Prueba 2 - Prompt estructurado

**Herramienta:** Claude

**Prompt:**

> # Rol
> Actúa como un estudiante universitario que se comunica de forma formal y respetuosa.
>
> # Contexto
> Debo entregar el informe del proyecto final del curso de Diseño de Interfaces el viernes, pero dos integrantes del equipo estuvieron enfermos esta semana.
>
> # Tarea
> Redacta un correo al docente solicitando una prórroga de 3 días.
>
> # Formato de salida
> Incluye asunto, saludo, cuerpo en máximo 2 párrafos y despedida.
>
> # Restricciones
> No exageres la situación, no uses más de 120 palabras y propone una nueva fecha concreta.

**Resultado (resumen):** Claude redactó un único correo formal al docente, en dos párrafos, con asunto, saludo y despedida. Pidió una prórroga de 3 días, del viernes 2 de octubre al lunes 5 de octubre, y mencionó a los dos integrantes enfermos sin exagerar.

**Observaciones (diferencias frente a la Prueba 1):**
- **Extensión:** el correo estructurado es más corto y respeta el máximo de 120 palabras (unas 95, según Claude); el vago ocupa más espacio porque incluye dos versiones.
- **Tono:** el estructurado suena a un estudiante formal y respetuoso, sin exagerar; el vago es genérico y de plantilla.
- **Precisión:** el estructurado usa el contexto real (informe, curso, enfermedad) y propone fechas concretas; el vago deja la fecha, el trabajo y el motivo entre corchetes.
- **Estructura:** el estructurado cumple asunto, saludo, 2 párrafos y despedida; el vago tiene estructura similar pero con opciones A y B y sin adaptarse a lo pedido.

---

## Prueba 3 - Zero-shot

**Herramienta:** Claude

**Prompt:**

> Clasifica cada comentario como POSITIVO, NEGATIVO o NEUTRO.
> 1. "La app se cierra cada vez que intento pagar."
> 2. "Llegó el pedido, nada que destacar."
> 3. "Me encantó lo rápido que cargan las pantallas."
> 4. "Está bien, aunque el botón de ayuda es difícil de encontrar."

**Resultado (resumen):** Clasificó el 1 como NEGATIVO, el 2 como NEUTRO, el 3 como POSITIVO y el 4 como NEUTRO, con una explicación breve para cada uno.

**Observaciones:** Al no tener ejemplos, el modelo solo pudo usar las tres categorías dadas. El comentario 4 (mezcla algo bueno con algo malo) no encajaba bien, así que puso NEUTRO y aclaró que también podría ser NEGATIVO. Además, respondió con una lista numerada y explicaciones largas, y no indicó ningún tema.

---

## Prueba 4 - Few-shot

**Herramienta:** Claude

**Prompt:**

> Clasifica cada comentario siguiendo el formato de los ejemplos.
>
> Comentario: "Excelente diseño, todo es muy intuitivo."
> Categoría: POSITIVO │ Tema: diseño
>
> Comentario: "Buen precio, pero la entrega tardó una semana."
> Categoría: MIXTO │ Tema: entrega
>
> Comentario: "La app se cierra cada vez que intento pagar."
> Categoría:
>
> Comentario: "Está bien, aunque el botón de ayuda es difícil de encontrar."
> Categoría:

**Resultado (resumen):** Clasificó el comentario 3 como NEGATIVO con tema "pago" y el comentario 4 como MIXTO con tema "ayuda".

**Observaciones:**
- **¿Respetó el formato?** Sí, usó exactamente `Categoría │ Tema`, igual que los ejemplos.
- **¿Identificó el tema?** Sí, indicó "pago" y "ayuda" en cada caso.
- **¿Usó MIXTO?** Sí, en el comentario 4, una categoría que solo aprendió del ejemplo.
- **Comparación con zero-shot:** la respuesta fue más corta y directa, sin explicaciones extra, y resolvió mejor el comentario ambiguo.

---

## Prueba 5 - Resumen con delimitadores

**Herramienta:** Claude

**Prompt:**

> Resume el texto delimitado por `<texto></texto>` en 3 viñetas de máximo 20 palabras cada una.
> Luego escribe una sola oración con la idea principal.
>
> `<texto>`
> Las interfaces de programación de aplicaciones, conocidas como APIs, permiten que dos sistemas se comuniquen entre sí sin que cada uno conozca los detalles internos del otro. Hoy en día, casi todas las aplicaciones móviles dependen de ellas: cuando una persona consulta el clima, paga un pedido o inicia sesión con su cuenta de Google, hay una API trabajando en segundo plano. Entre los estilos de diseño más usados destaca REST, que organiza los recursos mediante direcciones URL y utiliza los métodos HTTP como GET, POST, PUT y DELETE para leer, crear, actualizar o eliminar información. Una buena API REST usa nombres de recursos en plural, devuelve códigos de estado claros y mantiene un formato de respuesta consistente, generalmente JSON. Además, es importante versionar la API para no romper las aplicaciones que ya la utilizan cuando se introducen cambios. La seguridad también es un aspecto central: se recomienda autenticar las solicitudes con tokens, limitar la cantidad de peticiones por usuario y nunca exponer datos sensibles en las URL. Por último, una documentación clara y con ejemplos reales reduce el tiempo que otros desarrolladores necesitan para integrarse. Cuando estas prácticas se aplican desde el inicio, el mantenimiento resulta más sencillo, los errores se detectan más rápido y el producto puede crecer sin generar deuda técnica innecesaria.
> `</texto>`

**Resultado (resumen):** Claude devolvió 3 viñetas que resumen qué son las APIs, las prácticas de diseño REST y la seguridad con documentación, más una oración final con la idea principal sobre aplicar buenas prácticas desde el inicio.

**Observaciones:**
- Los delimitadores `<texto></texto>` funcionaron: el modelo entendió qué era instrucción y qué era el texto a resumir.
- Respetó el número de viñetas (3) y cerró con una sola oración de idea principal.
- No respetó el límite de 20 palabras: las viñetas tienen entre 21 y 22 palabras. Para resumir mucho contenido, juntó varias ideas en cada viñeta usando comas y punto y coma.
- Mejora posible: pedir "máximo 15 palabras" para dejar margen, o pedirle que cuente las palabras antes de responder.

---

## Prueba 6 - Extracción a tabla Markdown y JSON

**Herramienta:** Claude

**Prompt:**

> Del siguiente mensaje extrae: nombre, curso, fecha y motivo.
> Devuelve primero una tabla Markdown y después el mismo contenido en JSON válido.
> Si algún dato no aparece, escribe "no especificado".
>
> """
> Hola, soy Lucía Ramos del curso de Base de Datos. Quería avisar que el martes 14 no podré asistir al laboratorio porque tengo una cita médica.
> """

**Resultado (resumen):** Claude devolvió primero una tabla Markdown con los cuatro campos (nombre: Lucía Ramos, curso: Base de Datos, fecha: martes 14, motivo: cita médica) y después el mismo contenido en un bloque JSON.

**Observaciones:**
- Respetó el orden pedido: tabla primero y JSON después, con exactamente los mismos datos en ambos.
- El JSON es válido: usa llaves, comillas dobles y comas bien ubicadas.
- No inventó información: como el mensaje solo decía "martes 14", dejó la fecha así y agregó una nota aclarando que faltaban el mes y el año.
- La regla "no especificado" no se aplicó porque los cuatro datos aparecían en el texto.
- Las comillas triples separaron bien el mensaje de las instrucciones.

---

## Prueba 7 - Razonamiento paso a paso

**Herramienta:** Claude

**Prompt:**

> Tengo 3 tareas para esta semana:
> - Informe de laboratorio (4 h, entrega miércoles)
> - Estudiar para el examen (6 h, examen viernes)
> - Presentación grupal (3 h, jueves)
> Dispongo de 3 horas libres por día de lunes a jueves.
> Piensa paso a paso: primero calcula las horas disponibles, luego verifica si alcanzan y finalmente propone un horario día por día en una tabla.

**Resultado (resumen):** Claude calculó 12 horas disponibles frente a 13 necesarias, concluyó que faltaba 1 hora y propuso un horario de lunes a viernes: informe el lunes y martes, presentación el martes y miércoles, y estudio de miércoles a viernes, con la hora que faltaba el viernes antes del examen.

**Observaciones:**
- Mostró el razonamiento en tres pasos (horas disponibles, verificación y horario) antes de la tabla final, tal como se pidió.
- Los cálculos son correctos: 12 h disponibles, 13 h necesarias y 1 h de déficit.
- El horario respeta las fechas de entrega: el informe termina el martes y la presentación el miércoles, con un día de margen en ambos casos.
- Para cubrir el déficit propuso 1 h el viernes, fuera de las horas libres indicadas, y lo aclaró.
- Agregó un párrafo no solicitado sobre qué pasaría si ya había pasado el lunes, usando la fecha actual.
- Pedir "piensa paso a paso" hizo que detectara que el tiempo no alcanzaba antes de armar la tabla.

---

## Prueba 8 - Encadenamiento de prompts (misma conversación)

**Herramienta:** Claude

**Resultado (resumen):** Claude generó un índice de 5 secciones sobre buenas prácticas de APIs REST, desarrolló solo la sección 2 ("Diseño de recursos y endpoints") con reglas y un ejemplo `GET /usuarios/42/pedidos?estado=enviado`, y luego revisó esa sección proponiendo 3 mejoras de claridad.

**Observaciones:**
- La cadena funcionó: el Prompt 2 usó el índice del Prompt 1 sin que se lo repitiera, y el Prompt 3 revisó justo la sección que escribió el Prompt 2.
- Cada paso quedó enfocado en una sola tarea (planificar, producir, evaluar), lo que hizo las respuestas más fáciles de revisar.
- Prompt 1: respetó el máximo de 5 secciones y agregó una breve descripción de cada una.
- Prompt 2: desarrolló solo la sección 2 e incluyó el ejemplo de endpoint. Contando las palabras de la sección obtuve 105, frente a las 150 pedidas. Además agregó un bloque JSON de respuesta que no se había solicitado.
- Prompt 3: entregó exactamente 3 mejoras concretas (explicar el ejemplo, aclarar PUT vs PATCH y concretar la regla del anidamiento), citando partes reales del texto, más una sugerencia extra no pedida.
---

## Rúbrica de evaluación

| Criterio   | v1 | v2 | v3 |
|------------|----|----|----|
| Relevancia | 4  | 5  | 5  |
| Precisión  | 2  | 4  | 5  |
| Formato    | 3  | 3  | 4  |
| Tono       | 3  | 5  | 5  |
| **Total**  | **12/20** | **17/20** | **19/20** |

---

## Iteraciones - Descripción de un producto (botella térmica de acero inoxidable de 750 ml)

| Versión | Cambio realizado en el prompt      | Puntaje total |
| ------- | ---------------------------------- | :-----------: |
| v1      | Prompt inicial sin estructura      |     12/20     |
| v2      | Se agregó rol y contexto           |     17/20     |
| v3      | Se definió formato y restricciones |     19/20     |

**Prompt v1:**

> Escribe una descripción de una botella térmica.

**Prompt v2:**

> # Rol
> Actúa como redactor publicitario especializado en productos para estudiantes universitarios.
>
> # Contexto
> Vendo una botella térmica de acero inoxidable de 750 ml en una tienda online. Mantiene el frío hasta 24 horas y el calor hasta 12 horas. Mi público son estudiantes universitarios que pasan el día entre clases, biblioteca y transporte.
>
> # Tarea
> Escribe la descripción del producto.

**Prompt v3:**

> (Igual que v2, más lo siguiente)
>
> # Formato de salida
> Incluye un título de máximo 8 palabras, un párrafo de 2 a 3 oraciones y 3 viñetas de beneficios.
>
> # Restricciones
> Máximo 80 palabras en total, tono cercano y juvenil, no inventes datos técnicos que no te di y no hagas preguntas al final.

**Puntajes por criterio (Relevancia / Precisión / Formato / Tono):**
- v1: 4 / 2 / 3 / 3
- v2: 5 / 4 / 3 / 5
- v3: 5 / 5 / 4 / 5

**Qué se cambió y por qué:**
- **v1 → v2:** agregué rol y contexto porque v1 inventó datos (capacidades, colores, horas de temperatura) y usó un tono genérico. Con el contexto real usó mis datos y le habló a estudiantes.
- **v2 → v3:** agregué formato y restricciones porque v2 salió larga, con estructura elegida por el modelo y cerró con una pregunta. En v3 la estructura fue la pedida y desapareció la pregunta final.
- **Lo que quedó pendiente:** v3 se pasó un poco del límite de 80 palabras, lo que confirma que el modelo no cuenta palabras con exactitud.

---

## Plantilla: Redacción de correo formal

```text
Actúa como {{rol}}.
Contexto: {{situación}}.
Redacta un correo dirigido a {{destinatario}} para {{objetivo}}.
Formato: asunto, saludo, cuerpo en máximo {{n}} párrafos y despedida.
Restricciones: máximo {{palabras}} palabras, tono {{tono}}.
```

---

## Plantilla: Resumen con delimitadores

```text
Resume el texto delimitado por <texto></texto> en {{n_viñetas}} viñetas de máximo {{palabras}} palabras cada una.
Luego escribe una sola oración con la idea principal.
Dirige el resumen a {{público}}.

<texto>
{{texto_a_resumir}}
</texto>
```

---

## Plantilla: Clasificación con few-shot

```text
Clasifica cada comentario como {{categorías}} siguiendo el formato de los ejemplos.

Comentario: "{{ejemplo_1}}"
Categoría: {{categoría_1}} │ Tema: {{tema_1}}

Comentario: "{{ejemplo_2}}"
Categoría: {{categoría_2}} │ Tema: {{tema_2}}

Comentario: "{{comentario_nuevo}}"
Categoría:
```

---

## Plantilla: Extracción de datos a tabla y JSON

```text
Del siguiente mensaje extrae: {{campos}}.
Devuelve primero una tabla Markdown y después el mismo contenido en JSON válido.
Si algún dato no aparece, escribe "no especificado".

"""
{{mensaje}}
"""
```

---

## Conclusiones

- Un prompt vago obliga al modelo a adivinar: en la Prueba 1 devolvió una plantilla genérica con dos destinatarios posibles y datos por completar. Con los cinco componentes (rol, contexto, tarea, formato y restricciones), la Prueba 2 produjo un correo listo para usar, con fechas concretas y la estructura pedida.
- Los ejemplos del few-shot enseñaron al modelo el formato "Categoría │ Tema" y la categoría MIXTO sin explicarlas. En zero-shot, el mismo comentario ambiguo quedó en NEUTRO con dudas.
- Los delimitadores (`<texto></texto>` y comillas triples) separaron con claridad las instrucciones del contenido, y la regla "no especificado" evitó que el modelo inventara datos que no estaban en el mensaje.
- Pedir razonamiento paso a paso hizo que el modelo detectara que las horas no alcanzaban antes de proponer el horario, y el encadenamiento de prompts permitió planificar, producir y revisar en pasos pequeños y fáciles de controlar.
- En la iteración de la descripción de producto, el puntaje subió de 12/20 (v1) a 17/20 (v2) y 19/20 (v3), lo que muestra que cada componente agregado mejora el resultado.
- Una limitación que observé es que el modelo no siempre cumple los conteos exactos de palabras (por ejemplo, las viñetas del resumen y la descripción del producto se pasaron ligeramente del límite), por lo que conviene revisar esas restricciones a mano.
- En general, la calidad de la respuesta depende de la calidad del prompt, y documentar los prompts como plantillas reutilizables ahorra tiempo en tareas repetitivas.