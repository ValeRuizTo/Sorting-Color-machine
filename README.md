# Sorting-Color-machine
## 1. Resumen General

### Motivación
En la actualidad, los sistemas de manufactura enfrentan la necesidad de aumentar su productividad, flexibilidad y precisión, manteniendo bajos costos y garantizando la calidad del producto. La clasificación automática de piezas según atributos como el color es un proceso fundamental en múltiples industrias (alimentaria, farmacéutica, reciclaje, electrónica, etc.), donde la velocidad y confiabilidad de la separación impactan directamente en la eficiencia de la línea de producción.
La incorporación de tecnologías de Internet Industrial de las Cosas (IIoT) permite no solo automatizar la clasificación, sino también monitorear y recopilar datos en tiempo real, posibilitando análisis de desempeño, mantenimiento predictivo y escalabilidad del proceso.

### Justificación
El proyecto busca desarrollar un prototipo funcional de línea de clasificación de piezas por color, utilizando el kit Sorting Line with Color Detection 24V de Fischertechnik, con el fin de poder representar de forma práctica un proceso de control industrial real, integrar los principios de percepción (sensores), actuación (actuadores), computación (controlador) y conectividad propios del IIoT.
En la vida real serviria para hacer procesos de clasificación automática que son ampliamente utilizados en:
- Industria alimentaria: clasificación de frutas, vegetales o granos según color, maduración o defectos.
- Industria farmacéutica: separación de pastillas o cápsulas defectuosas.
- Industria de reciclaje: clasificación de plásticos, vidrios o metales según color para facilitar su reprocesamiento.
- Líneas de ensamblaje: control de calidad y separación de componentes en función de su acabado o características visuales.

#### Relevancia del proceso

Este proceso de clasificación es fundamental porque:
- Aumenta la eficiencia al reducir el tiempo y la intervención manual.
- Mejora la calidad mediante una inspección y separación más precisa.
- Escala fácilmente a diferentes volúmenes de producción.
- Reduce costos operativos asociados a errores humanos y reprocesamiento.
- Integra principios de IIoT, ya que los datos capturados por sensores pueden enviarse a la nube o sistemas SCADA para monitoreo, análisis predictivo y optimización del proceso.

### Objetivos del proyecto
#### Objetivo general
Diseñar, desarrollar, implementar y validar un prototipo automatizado de línea de clasificación de piezas por color, basado en principios de IIoT y utilizando el kit Fischertechnik Sorting Line with Color Detection 24V.
#### Objetivo especifico
- Identificar el proceso de control industrial y justificar su necesidad de automatización mediante revisión de antecedentes.
- Levantar y documentar las restricciones de diseño (técnicas, económicas, regulatorias, temporales y de escalabilidad).
- Diseñar la arquitectura de hardware y software que integre sensores, actuadores, controlador y conectividad.
- Implementar el prototipo físico en base al diseño establecido.
- Validar el funcionamiento mediante un protocolo de pruebas experimentales, evaluando desempeño y confiabilidad.
- Documentar los resultados obtenidos y proponer mejoras o líneas de trabajo futuro.

### Estructura de la documentación
- Resumen general: motivación, justificación, objetivos y estructura.
- Solución propuesta: restricciones de diseño, arquitectura planteada, desarrollo modular y estándares aplicados.
- Configuración experimental, resultados y análisis: entorno de pruebas, datos obtenidos y evaluación del desempeño.
- Autoevaluación del protocolo de pruebas: análisis crítico de la metodología empleada.
- Conclusiones y trabajo futuro: retos, aprendizajes y proyección del proyecto.Anexos: código fuente, esquemáticos y material complementario.

### Proceso seleccionado
El proceso industrial seleccionado corresponde a una línea de clasificación de piezas por color (Sorting Line with Color Detection 24V), desarrollada con los kits de Fischertechnik. Este sistema es representativo de un proceso típico de automatización en la industria manufacturera, en donde se requiere clasificar objetos en función de sus propiedades físicas detectadas mediante sensores.

### Descripción del proceso 
La línea de clasificación consiste en:

- Alimentación de piezas: Las piezas ingresan al sistema mediante una cinta transportadora motorizada.
- Percepción: Un sensor de color detecta la tonalidad de cada pieza en tiempo real.
- Computación y control: El controlador interpreta la señal del sensor, la procesa y toma una decisión de clasificación.
- Actuación: Dependiendo del color detectado, un actuador (p. ej., desviador o empujador neumático/eléctrico) redirige la pieza hacia la rampa o contenedor correspondiente.
- Salida: Las piezas se depositan en diferentes compartimientos, logrando la separación automática.

## 2. Solución Propuesta

### Restricciones de diseño

## 2. Solución Propuesta

### Restricciones de diseño


| Código | Tipo        | Nombre del Requerimiento | Descripción                                                                 | Prioridad | Viabilidad técnica                                                                 | Restricciones                                      | Recursos requeridos                        | Impacto                                               |
|--------|-------------|--------------------------|-----------------------------------------------------------------------------|-----------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------|--------------------------------------------|-------------------------------------------------------|
| RF-01  | Funcional   | Detección de color       | El sistema debe identificar piezas de al menos 3 colores distintos mediante el sensor óptico. | Alta      | El kit Fischertechnik incluye un sensor de color analógico calibrable para distinguir múltiples tonos. | Limitado al espectro soportado por el sensor       | Sensor óptico de color                     | Permite clasificación automática.                     |
| RF-02  | Funcional   | Clasificación automática | El sistema debe desviar cada pieza hacia el contenedor correspondiente según su color. | Alta      | El kit dispone de compresor, válvulas y actuadores neumáticos que permiten desviar las piezas con precisión. Así como fototransistores para garantizar la presencia de los objetos y la sincronización del sistema | Número de salidas limitado a 3 contenedores      | Motores, válvulas, compresor y fototransistores              | Representa el proceso industrial de sorting.          |
| RF-03  | Funcional   | Registro de datos        | El sistema debe enviar el resultado de clasificación (color detectado y cantidad de piezas) a un servidor IoT. | Media     | El controlador TXT/PLC puede comunicarse vía Ethernet/WiFi con un servidor externo, aunque requiere configuración adicional.  | Depende de conectividad disponible                 | Controlador con WiFi/Ethernet, servidor IoT| Integra IIoT y análisis remoto.                       |
| RF-04  | Funcional   | Interfaz de monitoreo    | El usuario debe visualizar en tiempo real la operación (colores detectados, conteo, estado de actuadores). | Media     |  Existen plataformas como Node-RED o Grafana que pueden integrarse con el controlador para mostrar datos en dashboards simples. Inicialmente, se muestran datos básicos en el display del controlador.| Requiere desarrollo de software adicional          | Node-RED, Grafana o app web                | Mejora la usabilidad y monitoreo remoto.              |
| RNF-01 | No funcional| Limitación de energía    | El prototipo debe funcionar con fuentes de 9V o 24V según kit disponible.   | Media      |  Ambos voltajes están soportados oficialmente por Fischertechnik, y se dispone de fuentes de laboratorio. | Depende de disponibilidad de fuente y controlador  | Fuente de poder, adaptadores               | Asegura compatibilidad con componentes Fischertechnik. |
| RNF-02 | No Funcional | Mantenibilidad | El sistema debe estar diseñado de forma modular para facilitar el reemplazo de sensores, actuadores o controladores sin necesidad de rediseñar todo el prototipo. | Baja |  los kits de Fischertechnik son modulares y permiten intercambiar componentes fácilmente. | Limitado a la compatibilidad de módulos disponibles en el kit. | Herramientas básicas, repuestos del kit. | Impacta en la sostenibilidad y reutilización del prototipo a largo plazo. |
| RNF-03 | No funcional| Escalabilidad            | El sistema debe permitir la ampliación hacia más colores o integración con otros módulos. | Baja     |  El controlador dispone de entradas/salidas adicionales que permiten integrar más sensores o módulos industriales. | Limitado por número de sensores/entradas del controlador | PLC o controlador con entradas libres     | Facilita futuras expansiones del proyecto.            |

Nota: Debido a que el kit no pudo ser energizado durante el desarrollo, no fue posible realizar pruebas prácticas de los sensores, actuadores y controlador. Por ello, la evaluación de viabilidad presentada es preliminar y se fundamenta en la documentación técnica y antecedentes. La validación experimental se realizará una vez se pueda poner en marcha el prototipo.


### Arquitectura propuesta

Diagrama de bloques (hardware y software)

### Desarrollo teórico modular

#### Criterios de diseño establecidos

#### Diagramas UML (arquitectura general y módulos de software)

#### Esquemáticos de hardware diseñados

#### Estándares de diseño aplicados

## 3. Configuración Experimental

#### Metodología experimental

#### Resultados obtenidos

#### Análisis de resultados

## 4. Autoevaluación del Protocolo de Pruebas

#### Metodología de validación

#### Limitaciones del protocolo

#### Mejores prácticas identificadas

## 5. Conclusiones y Trabajo Futuro

#### Conclusiones principales

#### Retos durante el desarrollo

#### Líneas de trabajo futuro

## 6. Anexos

#### Código fuente documentado

#### Esquemáticos de hardware

Material complementario (diagramas, tablas, referencias)
