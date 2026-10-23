# Diseño y construcción de una incubadora neonatal a escala
Instrumentación Biomédica y Biosensores, Ingeniería Biomédica, UMNG (Semestre VII).

## Integrantes
- Ana Sofia Conde Porras - 5600770
- Antonia Garzón Vanegas - 5600843
- María José Peña Velandia - 5600876

## Objetivo general
Reconocer la importancia de la incubadora neonatal

## Objetivos específicos
- Reconocer las variables físicas involucradas en la incubadora neonatal.
- Desarrollar un sistema que simule la báscula y la temperatura de una incubadora real.
- Evaluar cómo impacta el control de variables como temperatura, humedad y
flujo de aire en la salud del neonato.

## Resumen de la práctica 
Se diseñó y construyó un prototipo a escala de una incubadora neonatal con dimensiones de 44 cm × 20 cm × 22 cm (mínimas requeridas por el docente), para emular el control y monitoreo de variables fisiológicas de un recién nacido. El sistema incorporó un sensor DHT11 para la medición de temperatura y humedad relativa, una galga extensométrica para el registro de peso y un bombillo actuando como elemento calefactor. La adquisición, acondicionamiento y visualización local de los datos se realizaron mediante un circuito electrónico integrado a una tarjeta Arduino Uno y una pantalla OLED. Asimismo, se desarrolló un script en MATLAB para el procesamiento digital y análisis de las señales obtenidas.

## Estructura del repositorio
- Parte A = Diseño y simulación  
  Identificación de los componentes y revisión bibliográfica de las partes de una incubadora  
  Control de temperatura: Esquema y simulación del control de lazo cerrado (36 °C - 37.5 °C)  
  Medición de peso: Circuito de acondicionamiento y simulación para la galga extensométrica  
  
- Parte B = Prototipo y Software  
  Código de Arduino: Script (.ino) para DHT11, galga, pantalla OLED y actuadores  
  Código de Matlab: Script (.m) para recepción y procesamiento de datos
  Esquemáticos y montaje: Circuito físico e infraestructura a escala (44 cm x 20 cm x 22 cm)  
  Estudio financiero: Costos detallados y comparativa con mercado (Dräger, LEEX, etc.)
  
- Parte C = Análisis y resultados  
  Evaluación y desempeño: Análisis de error en peso patrón y precisión térmica  
  Preguntas y discusión: Respuestas al cuestionario guía (variables, servo-cuna, etc.)  
  Conclusiones: Síntesis del proyecto y reflexiones técnicas  

## Conclusión general
FALTA POR HACER 

# Parte A — Diseño y simulación
