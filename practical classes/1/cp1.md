
## Guía CP 1

### Introducción
- Recordar algunos conceptos de la conferencia, a través de preguntas
  - Sistema (objeto de la investigación), entidades, relaciones y procesos
  - Tipos de sistemas (naturales, socio-políticos, tecnológicos, etc.)
  - Modelo (distintos niveles de abstracción) 
  - Simulación (qué es)
  - Simulación computacional
  - Sistemas dinámicos: estacionarios y no estacionarios
  - Relación sistema- medio
  - Sistemas deterministas y no deterministas

- Por qué son importantes las simulaciones
  - los experimentos reales son impracticables debido a su escala temporal y espacial. Por ejemplo, en astrofísica, es imposible estudiar el ciclo de vida de una galaxia.
  - Los experimentos reales son peligrosos, costosos o inmorales. Por ejemplo, en medicina, no se pueden hacer experimentos con humanos.
  - Los experimentos reales son imposibles de repetir. Por ejemplo, en geología, no se puede repetir la formación de una montaña.
  - Los experimentos reales pueden ser en extremo costosos. Por ejemplo, la estabilidad de una construcción, estrategias de guerra, etc. 
  - problema para el que no existe una solución analítica

### Desarrollo
- Casos de uso de las simulaciones

- Pipeline de una simulación
  - Modelado: Necesitamos un modelo, descripción formal del problema donde se extraigan las características relevantes del sistema.
  - Modelado a nivel computacional: El modelo debe ser preprocesado, de forma tal que sea compatible con la plataforma en la que se va a implementar, una computadora en el caso de las simulaciones computacionales
  - Implementación: Los algoritmos computacionales deben ser implementados en un lenguaje de programación, de forma que sean eficientes y siguiendo las buenas prácticas de programación.
  - Exploración de datos: Los datos resultantes de una simulación deben ser interpretados. En algunos casos, por ejemplo para cantidades escalares, esto será fácil, en otros, por ejemplo para conjuntos de datos de alta dimensión, extraer la información relevante es una tarea científica importante. 
  - Validación de los resultados: 
    - Qué tan confiables son los resultados de la simulación? 
    - Identificar posibles fuentes de error
    - Comparar con otros modelos, experimentos o teorías
    - A partir de aquí se puede volver a comenzar el pipeline, si los resultados no son satisfactorios.
  - Embedding: Las simulaciones no son un fin en sí mismas, sino que se realizan en un contexto y deben ser integradas en él. 
 Esto puede requerir la definición de interfaces, un razonable diseño de software, entornos de prueba simples, etc.


- Explicar metodología para diseñar una simulación. Puede ser a través de un caso de uso.

- Dinámica de grupo "Casos de uso de las simulaciones": 

   Se forman grupos de aproximadamente 6 estudiantes y se les pide que propongan un problema que les interese resolver y en el que crean que sea conveniente utilizar simulación. Se les da 10 minutos para discutirlo y 5 minutos para presentar su problema y solución propuesta (3 minutos para presentar y 2 minutos para preguntas).

   Alternativas:
    - Se les da un problema y se les pide que propongan una solución
    - Se elabora un listado de problemas entre todo el grupo y luego se asignan a los equipos.

### Conclusiones
- Take home message: 
    - Las simulaciones son una herramienta poderosa para el estudio de sistemas complejos
    - El mapa no es el territorio
    - Las simulaciones complementan los análisis teóricos y los experimentos, no los reemplazan.