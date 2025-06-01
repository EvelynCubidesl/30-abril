# Proyecto de Simulación de Transmisión Mecánica en Simscape Multibody

Este repositorio documenta la simulación y análisis de distintos mecanismos de transmisión mecánica utilizando **Simulink** y **Simscape Multibody**, como parte de un estudio de control y dinámica aplicado a sistemas como tornillo sin fin, piñón-cremallera y bandas transportadoras.
![image](https://github.com/user-attachments/assets/e37d44e1-ef8a-4aa0-bbb5-9a3881af07e3)

## Contexto del Proyecto

El proyecto parte de una experiencia real con un banco de pruebas de la Fuerza Aérea, que usaba una cabina con controles mecánicos conectados por guayas a una turbina **PT6**. Los problemas de precisión y backslash motivaron el análisis de sistemas de transmisión alternativos más eficientes y con mejor respuesta.

### Mecanismos Simulados

## Sistema de Engranajes
# Definición
Un sistema de engranajes transmite movimiento rotacional entre ejes mediante el contacto directo de dientes. Es ampliamente utilizado para modificar velocidad, torque e inercia reflejada.
![image](https://github.com/user-attachments/assets/c44a5bc0-dcd8-4664-aaef-a55460c95bce)

# Relación de Transmisión
La relación de transmisión entre dos engranajes está dada por:
# Inercia Reflejada
La inercia reflejada hacia el eje del motor se calcula como: `J_reflejada = J_carga * (1 / relación)^2`

# Torque Reflejado
El torque reflejado se ajusta por la relación de transmisión, pero no se eleva al cuadrado: `T_reflejado = T_carga * 1 / relación`

# Eficiencia
La eficiencia del sistema depende del tipo de engranaje y su lubricación. En control de movimiento, se busca minimizar pérdidas para mantener la precisión.

![image](https://github.com/user-attachments/assets/3fbc6c46-9083-4497-993c-dc0fb772f00d)
**simulacion de engranajes**

 Sistema Polea-Correa
# Definición
Es un mecanismo que transmite movimiento rotacional entre dos ejes mediante una correa flexible. Puede ser:
- Liso: fricción entre correa y polea.
- Dentado: sincronización precisa sin deslizamiento.
![image](https://github.com/user-attachments/assets/3d58ee58-73d6-4cae-ad78-60de3a08020d)

# Relación de Transmisión
Basada en el radio de las poleas: 
`ω1 / ω2 = r2 / r1` ,

# Inercia Reflejada
Similar a los engranajes, pero se debe considerar la masa de la correa como una inercia rotacional adicional: "Igual que en engranajes.",

#Torque Reflejado
Se comporta igual que en engranajes: "Igual que en engranajes.",

# Eficiencia
Las correas dentadas tienen mayor eficiencia y precisión que las lisas. La eficiencia también depende de la tensión y el tipo de material.

![image](https://github.com/user-attachments/assets/ddf9891d-47d7-4047-b80c-cb387d611258)
simulacion correa polea

### Piñón-Cremallera
# Definicion:
Es un mecanismo muy común para convertir movimiento rotacional en movimiento lineal. Consiste en un engranaje circular (piñón) que engrana con una barra dentada lineal (cremallera). Al girar el piñón, la cremallera se desplaza linealmente.

![image](https://github.com/user-attachments/assets/01a5b3c5-c728-471f-b5cd-fbe035158d52)

- Muy usado en la industria por su facilidad de diseño y eficiencia.
- Relación de transmisión: `"v = r * ω`
- Inercia reflejada: igual que en el tornillo, pero sin reflejar el piñón (acoplado al motor directamente).
- Se usó el bloque de piñón-cremallera de Simscape para simular el desplazamiento lineal.

![image](https://github.com/user-attachments/assets/456449c0-e3aa-4f5c-aa9c-c0b906c679f8)
simulacion  piñon cremallera 

### Tornillo Sin Fin

# Definicion  Es un mecanismo ampliamente usado para convertir movimiento rotacional (del motor) en movimiento lineal. Los tipos más comunes son los tornillos ACME y los tornillos de esferas. Estos últimos permiten transmitir grandes potencias con alta eficiencia (85%–95%) y menor fricción, gracias a que actúan como rodamientos.


- Transforma movimiento rotacional en lineal.
- Se modeló considerando:
  - Relación de transmisión: `ω / v = 2π / paso`
  - Inercia total: suma de la inercia del tornillo + carga reflejada + carro
  - Eficiencia del sistema "Se calcula a partir de la energía cinética lineal transformada a rotacional."
  - "Torque reflejado": "Se calcula considerando la eficiencia y la fuerza lineal."
  
![image](https://github.com/user-attachments/assets/6b29bddb-0b8b-48b7-9ea9-0262392c42d9)
![image](https://github.com/user-attachments/assets/bdf006d8-6f2e-4f47-91b6-a2ebb418a895)
Simulacion tornillo sin fin

### Banda Transportadora
# Definicion Es un sistema muy utilizado para generar movimiento lineal a partir de una fuente de movimiento rotacional, como un motor. En su forma más simple, la banda conecta dos poleas (generalmente de igual radio), y puede incluir rodillos locos para soportar cargas más ligeras o trayectos más largos.

- Similar a poleas-correas, pero permite múltiples poleas y salida lineal.
- Inercia total:
  - Polea motriz
  - Carga y carro
  - Masa de la banda
- Relación de transmisión depende del radio de la polea motriz.
![image](https://github.com/user-attachments/assets/3426eaf6-9ee4-4d2b-879f-5c57fd65256f)

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


