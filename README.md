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

# Parte A - Diseño y simulación
# Parte B - Prototipo y Software
### Descripción técnica del circuito de la incubadora neonatal a escala
El prototipo desarrollado integra un sistema de monitoreo y control de temperatura, un mecanismo de ventilación, un sistema de medición de peso y una interfaz de visualización. Su funcionamiento se basa en la adquisición de señales mediante sensores, el procesamiento de la información con un microcontrolador Arduino Uno y la activación de actuadores mediante un módulo de relé de dos canales.
#### 1. Alimentación y unidad de procesamiento
El circuito incorpora una fuente de alimentación de corriente continua de 12 V para suministrar energía a los componentes que requieren este nivel de tensión. El Arduino Uno actúa como unidad de procesamiento y control, ejecutando las instrucciones programadas para interpretar las señales de los sensores, gestionar los indicadores luminosos y controlar los actuadores.

El sistema también utiliza un módulo de relé de dos canales, cuyas entradas de control IN1 e IN2 están conectadas a los pines digitales 7 y 8 del Arduino Uno, respectivamente. Este módulo permite conmutar circuitos eléctricos externos a partir de señales de control del microcontrolador.

La alimentación de cada componente debe ajustarse a sus especificaciones eléctricas, diferenciando la alimentación de corriente continua del circuito de control de la alimentación de corriente alterna utilizada por el bombillo.
#### 2. Sistema de monitoreo y control de temperatura
Para medir la temperatura interna de la incubadora se utiliza un sensor DHT11, que permite obtener mediciones de temperatura y humedad relativa. La información de temperatura es procesada por el Arduino Uno y comparada con los umbrales definidos en el programa de control.

A partir de esta comparación, el sistema activa tres indicadores luminosos que permiten identificar visualmente el estado térmico de la incubadora:
- LED azul: indica una temperatura inferior al rango establecido.
- LED verde: indica que la temperatura se encuentra dentro del rango deseado.
- LED rojo: indica una temperatura superior al límite establecido.
El elemento calefactor consiste en un bombillo incandescente de 100 W, alimentado mediante una conexión a la red eléctrica de corriente alterna. La energía eléctrica consumida por el bombillo se transforma parcialmente en calor, que contribuye al aumento de la temperatura en el interior de la estructura.

Para controlar el calentamiento y la ventilación se utiliza el módulo de relé. Según el montaje descrito, uno de sus canales participa en la conmutación de la alimentación del ventilador y el otro en la conexión del bombillo.

Cuando la temperatura supera el umbral programado, el Arduino puede activar el relé correspondiente para encender el ventilador. Este favorece la circulación del aire y contribuye a reducir la acumulación de calor. La respuesta del sistema depende de los umbrales y de la lógica implementada en el programa.

Por tanto, el control térmico se basa en la medición de temperatura, el procesamiento de la señal, la comparación con los valores de referencia y la activación de los actuadores.
#### 3. Etapa de conmutación mediante relés
El módulo de relé constituye la interfaz entre las señales de control de baja tensión del Arduino y los circuitos de potencia de los actuadores.

En el primer canal, el terminal común COM1 se conectó al positivo de 12 V y el contacto normalmente abierto NO1 se conectó a uno de los terminales del ventilador, de acuerdo con la descripción del montaje.

En el segundo canal se utilizó un contacto del relé para conmutar uno de los conductores de alimentación del bombillo. El bombillo se instaló en una roseta conectada a un cable de alimentación para la red eléctrica.

Cuando se activa la bobina del relé correspondiente, el contacto normalmente abierto se conecta al terminal común, permitiendo el paso de corriente por el circuito de la carga. Cuando el relé se desactiva, el contacto vuelve a su estado abierto.

Esta configuración permite controlar los actuadores sin utilizar directamente las salidas digitales del Arduino para alimentar sus cargas.

**Consideración de seguridad:** el circuito del bombillo opera con tensión de red, que es peligrosa. La separación eléctrica entre el circuito de control y el de potencia, el aislamiento de las conexiones y la protección contra contactos accidentales son fundamentales. El montaje debe verificarse con el docente antes de volver a energizarlo.
#### 4. Sistema de medición del peso
Para estimar la masa de un objeto colocado sobre la plataforma se incorporó una galga o sensor de fuerza. Este elemento responde a la carga aplicada mediante una variación eléctrica que debe ser interpretada por el sistema de adquisición.

En el prototipo se realizaron pruebas con diferentes configuraciones de conexión, buscando obtener una lectura de peso más sensible. Sin embargo, debido a que los valores medidos presentaron diferencias respecto a las masas de referencia, el sistema no se consideró completamente calibrado.

Durante las pruebas, una masa de referencia de 1800 g produjo una lectura de 2305 g. El error absoluto fue de 505 g y el error porcentual, calculado respecto a la masa de referencia, fue del 28,06 %.

Este resultado evidencia la necesidad de mejorar la calibración y la adquisición de la señal del sensor para aumentar la exactitud de las mediciones.
#### 5. Interfaz de visualización mediante pantalla OLED
El prototipo incorpora una pantalla OLED para visualizar el valor de peso calculado por el sistema.

La pantalla se comunica con el Arduino Uno mediante las líneas SDA y SCL, correspondientes a los datos y al reloj del protocolo de comunicación, si ese es el protocolo utilizado por el módulo. También dispone de conexiones de alimentación y tierra.

El Arduino procesa la información disponible del sensor de fuerza y actualiza el valor mostrado en la pantalla. De esta forma, la interfaz permite consultar directamente el resultado de la medición.
#### 6. Funcionamiento integrado del prototipo
El funcionamiento general del sistema puede describirse mediante la siguiente secuencia:
1. El sensor DHT11 adquiere información sobre la temperatura y la humedad relativa.
2. El Arduino Uno procesa la lectura de temperatura y la compara con los umbrales programados.
3. Los indicadores LED muestran el estado térmico identificado.
4. Cuando la temperatura supera el umbral definido, el Arduino activa el relé que controla el ventilador.
5. El bombillo incandescente actúa como fuente de calor y el ventilador favorece la circulación del aire.
6. El sensor de fuerza responde a la carga aplicada sobre la plataforma.
7. El sistema electrónico procesa la señal disponible y presenta el valor de peso en la pantalla OLED.
