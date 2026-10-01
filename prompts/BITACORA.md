# Bitacora de tecnicas avanzadas

Laboratorio 07: Tecnicas Avanzadas de Prompting.
Herramienta de IA usada: Gemini


## Ejercicio 2: Zero-shot, one-shot y few-shot

| Tipo | Aciertos (de 5) | Formato de la respuesta | Todas con el mismo formato (Si/No) |
|---|---|---|---|
| Zero-shot | 5 | Texto libre con explicaciones y numeración | No |
| One-shot | 5 | Intento de imitar flechas con texto adicional | Si |
| Few-shot | 5 | Estricto "texto -> etiqueta" por línea | Si |


## Ejercicio 3: Chain of Thought

| Pedido | Respuesta de la IA | Muestra los pasos (Si/No) | Correcta (Si/No) |
|---|---|---|---|
| Directo | 318.60 | No | Si |
| Paso a paso | Muestra descuento (90), IGV (106.20) y total (318.60) | Si | Si |

Ver el razonamiento paso a paso me permite auditar cada operación intermedia y detectar exactamente dónde ocurrió un fallo si el resultado final fuera incorrecto. Además, forzar al modelo a calcular de manera secuencial reduce la probabilidad de sesgos o errores en problemas matemáticos complejos.


## Ejercicio 4: Role prompting

| Version | Vocabulario (sencillo/tecnico) | Usa ejemplos o codigo | A quien le sirve mas |
|---|---|---|---|
| A. Sin rol | Neutral / Estándar | Ejemplos teóricos básicos | A cualquier persona que busque un concepto general |
| B. Rol docente | Sencillo | Analogías (ej. caja con etiqueta) | A principiantes o estudiantes sin experiencia |
| C. Rol senior | Técnico | Términos de memoria, tipos de datos y código en Java | A programadores o profesionales de desarrollo |

**Observación:** Asignar un rol no añade información nueva a la IA, sino que ajusta el tono, el nivel de abstracción, el vocabulario técnico y la audiencia a la que va dirigida la explicación.

## Ejercicio 5: Descomposicion

- **Paso 1:** Entregó los 5 requisitos del sistema de inventario (registro, consulta, actualización, eliminación y alertas de stock).
- **Paso 2:** Diseñó las clases necesarias (`Producto`, `Categoria`, `Inventario`) detallando sus atributos y tipos de datos.
- **Paso 3:** Generó el código en Java de la clase `Producto` estructurado con atributos privados, constructor y métodos getter/setter.
- **Paso 4:** Propuso 3 mejoras concretas: validación en setters, método `toString()` y uso de la API Date/Time para fechas de registro.

**Comparación:** El pedido de una sola vez generó un resultado genérico y superficial. En cambio, dividir la tarea por pasos permitió refinarla en cada nivel, obteniendo un código en Java más detallado, libre de ambigüedades y adaptado a las necesidades reales del proyecto.

## Ejercicio 6: Prompt estructurado y autocritica

### Prompts utilizados

```text
<rol>Actua como analista de pruebas de software.</rol>
<contexto>Login web con correo y contrasena. La cuenta se bloquea despues de 3 intentos fallidos.</contexto>
<tarea>Piensa paso a paso que puede fallar y escribe 6 casos de prueba.</tarea>
<formato>Tabla con las columnas: ID, escenario, datos de entrada, resultado esperado.</formato>

[Autocrítica solicitada]
Revisa tu tabla: faltan casos limite como campos vacios, correo sin @ o contrasena con espacios? Agrega los que falten e indica cuales agregaste.

