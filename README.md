# Proyecto de Simulación de Transmisión Mecánica en Simscape Multibody

Este repositorio documenta la simulación y análisis de distintos mecanismos de transmisión mecánica utilizando **Simulink** y **Simscape Multibody**, como parte de un estudio de control y dinámica aplicado a sistemas como tornillo sin fin, piñón-cremallera y bandas transportadoras.

## Contexto del Proyecto

El proyecto parte de una experiencia real con un banco de pruebas de la Fuerza Aérea, que usaba una cabina con controles mecánicos conectados por guayas a una turbina **PT6**. Los problemas de precisión y backslash motivaron el análisis de sistemas de transmisión alternativos más eficientes y con mejor respuesta.

## Mecanismos Simulados

### Tornillo Sin Fin

- Transforma movimiento rotacional en lineal.
- Se modeló considerando:
  - Relación de transmisión: `2π / paso`
  - Inercia total: suma de la inercia del tornillo + carga reflejada + carro
  - Eficiencia del sistema
- Ejemplo: carga de 50 kg, tornillo de acero, paso de 0.75 rev, eficiencia del 90%.

### Piñón-Cremallera

- Muy usado en la industria por su facilidad de diseño y eficiencia.
- Relación de transmisión: `1 / radio del piñón`
- Inercia reflejada: igual que en el tornillo, pero sin reflejar el piñón (acoplado al motor directamente).
- Se usó el bloque de piñón-cremallera de Simscape para simular el desplazamiento lineal.

### Banda Transportadora

- Similar a poleas-correas, pero permite múltiples poleas y salida lineal.
- Inercia total:
  - Polea motriz
  - Carga y carro
  - Masa de la banda
- Relación de transmisión depende del radio de la polea motriz.

## Modelado en Simscape

- Uso de bloques como:
  - **Prismatic Joint**
  - **Worm Gear / Lead Screw**
  - **Rack and Pinion**
  - **Rigid Transform**
  - **Weld Joint**
- Importancia de definir correctamente los *frames* para alinear componentes.
- Se visualizó el movimiento de cada parte usando sensores de posición y velocidad.

## Consideraciones de Diseño

- Importancia de diseñar correctamente mecanismos (evitar backslash).
- Simulación estructural previa (ej. en SolidWorks) para validación mecánica.
- Reflejo de masas e inercias esenciales para cálculos de torque y selección de actuadores.

## Resultados

- Se graficaron los desplazamientos rotacionales y lineales.
- Se evaluó la respuesta dinámica de los sistemas con diferentes cargas.
- Se compararon las eficiencias y comportamientos de los distintos mecanismos.

---

## Conclusión

El análisis demuestra cómo distintas configuraciones mecánicas afectan la precisión, eficiencia y respuesta dinámica del sistema. El uso de Simscape Multibody permite una comprensión detallada del impacto físico y controlable de cada elemento.


