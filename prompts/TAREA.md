# Tarea: Mi prompt avanzado

## Tarea elegida

Generar casos de prueba para el formulario de registro de usuarios de una aplicación web (campos: nombre, correo, contraseña y confirmación de contraseña). Elegí esta tarea porque es algo que hago con frecuencia en desarrollo y porque se puede evaluar fácilmente si la respuesta es completa y útil.

## Version 1: prompt basico

```text
Genera casos de prueba para un registro de usuarios.
```

**Técnica agregada:** ninguna (prompt base).

**Resultado observado:** [Describe qué respondió la IA: ¿cuántos casos dio? ¿en qué formato? ¿qué faltó? Ejemplo: "dio una lista corta y genérica, sin datos de entrada concretos ni resultado esperado".]

## Version 2

```text
Actúa como ingeniero QA con 8 años de experiencia en pruebas funcionales de aplicaciones web.

Contexto: el formulario de registro tiene los campos nombre, correo, contraseña y confirmación de contraseña. La contraseña debe tener mínimo 8 caracteres, una mayúscula y un número.

Genera casos de prueba para este formulario. Organízalos en tres secciones: casos válidos, casos inválidos y casos límite.
```

**Técnica agregada:** role prompting (rol específico) y prompt estructurado (contexto + secciones).

**Por qué la agregué:** en la versión 1 la respuesta fue genérica porque la IA no conocía las reglas del formulario ni el nivel de detalle esperado. El rol y el contexto la orientan a un perfil concreto y a reglas reales.

**Qué mejoró:** [Describe qué cambió: ¿ya separó válidos/inválidos/límite? ¿usó las reglas de contraseña? ¿Qué sigue faltando? Ejemplo: "los casos son más específicos, pero cada uno tiene un formato distinto y no incluye el resultado esperado".]

## Version 3: prompt final

```text
ROL: Eres un ingeniero QA con 8 años de experiencia en pruebas funcionales de aplicaciones web, especializado en validación de formularios.

CONTEXTO: El formulario de registro tiene los campos nombre, correo, contraseña y confirmación de contraseña. Reglas: la contraseña debe tener mínimo 8 caracteres, una mayúscula y un número; el correo debe tener formato válido y no estar repetido.

TAREA: Genera casos de prueba para este formulario. Sigue estos pasos:
1. Identifica las reglas de validación de cada campo.
2. Para cada campo, genera casos válidos, inválidos y límite.
3. Agrega al menos 2 casos que combinen varios campos.

FORMATO DE RESPUESTA: Una tabla en Markdown con las columnas ID, Campo, Tipo (válido/inválido/límite), Dato de entrada, Resultado esperado. Entre 12 y 15 casos en total.

EJEMPLO DEL FORMATO ESPERADO:
| ID | Campo | Tipo | Dato de entrada | Resultado esperado |
|----|-------|------|-----------------|--------------------|
| CP-01 | Contraseña | Límite | "Abcdef1" (7 caracteres) | Rechazada: mínimo 8 caracteres |

AUTOCRÍTICA: Al terminar, revisa tu propia tabla y responde en una sección aparte: ¿qué regla o caso importante no cubriste? Si encuentras alguno, agrégalo.
```

**Técnicas agregadas:** few-shot (ejemplo de fila), descomposición (pasos 1 a 3), formato de respuesta definido y autocrítica.

**Por qué las agregué:** en la versión 2 el formato de los casos era inconsistente y se omitían resultados esperados. El ejemplo fija el formato, los pasos obligan a cubrir cada campo y la autocrítica detecta lo que se le pasó.

**Qué mejoró:** [Describe: ¿la tabla salió con el formato pedido? ¿cuántos casos? ¿la autocrítica encontró algo nuevo?]

## Tecnicas usadas en el prompt final

| Técnica | Parte del prompt final que la aplica |
|---------|--------------------------------------|
| Role prompting | `ROL: Eres un ingeniero QA con 8 años de experiencia... especializado en validación de formularios.` |
| Prompt estructurado | Secciones `ROL`, `CONTEXTO`, `TAREA`, `FORMATO DE RESPUESTA`, `EJEMPLO` y `AUTOCRÍTICA` |
| Few-shot | `EJEMPLO DEL FORMATO ESPERADO` (fila CP-01 de la tabla) |
| Descomposición | Los pasos 1, 2 y 3 dentro de `TAREA` |
| Autocrítica | La sección `AUTOCRÍTICA` al final del prompt |

## Evaluacion del resultado

| Criterio | ¿Cumple? (Sí / No) |
|----------|--------------------|
| La respuesta usa exactamente el formato de tabla pedido | Sí |
| Cubre los cuatro campos del formulario | Sí |
| Incluye casos válidos, inválidos y límite | Sí |
| Cada caso tiene un resultado esperado claro | Sí |
| La autocrítica identifica al menos un caso faltante | Sí |

## Por que elegi estas tecnicas

Elegí role prompting porque necesitaba que la IA adoptara la mentalidad de un QA enfocado en cobertura de pruebas. El prompt estructurado permitió separar claramente el contexto de las reglas y la tarea. Aplicar few-shot solucionó el problema de formato de la versión 2, obligando a la IA a seguir la estructura exacta de la tabla. Usé descomposición para forzar que la IA no se centrara solo en la contraseña, sino en todos los campos e interacciones del formulario. Finalmente, la autocrítica actuó como un filtro de calidad para capturar posibles escenarios olvidados antes de dar por terminada la respuesta.

