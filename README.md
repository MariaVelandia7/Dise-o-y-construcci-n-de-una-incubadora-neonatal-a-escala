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

# Parte A - Diseño y simulación
## Fundamentos fisiologicos
El neonato, especialmente el prematuro, presenta una elevada superficie corporal en relación con su peso, piel delgada con barrera inmadura, poca grasa aislante, capacidad limitada para tiritar, control nervioso inmaduro y reservas energéticas reducidas. Estas características aumentan la pérdida de calor y dificultan mantener una temperatura estable [4, 14, 15].

### Balance térmico.
La temperatura neonatal depende del equilibrio entre la producción y la pérdida de calor. Esta última ocurre por cuatro mecanismos: conducción (contacto con superficies frías), convección (aire en movimiento), radiación (superficies frías cercanas) y evaporación (agua que se pierde por la piel y las vías respiratorias). La incubadora reduce estas pérdidas mediante aislamiento, circulación controlada de aire caliente y regulación de la humedad.

### Grasa parda.
Es una fuente importante de calor en el neonato y se localiza principalmente en la nuca, la región interescapular, las axilas y alrededor de los riñones. Ante el frío, la noradrenalina activa este tejido, que genera calor mediante el consumo de oxígeno y glucosa [15]. Los prematuros poseen reservas menores, lo que limita su capacidad de termorregulación.

### Ambiente térmico neutro.
Es el rango de temperatura ambiental en el que el neonato mantiene su temperatura corporal con el menor consumo de oxígeno y energía. Depende del peso, la edad gestacional y la edad posnatal; generalmente, cuanto menor es el peso y la madurez, mayores son los requerimientos térmicos. La incubadora busca mantener estas condiciones.

### Estrés por frío. 
Cuando la pérdida de calor supera su producción, el neonato aumenta el consumo de oxígeno y glucosa. Esto puede provocar hipoglucemia y acidosis metabólica. La acidosis y la hipotermia pueden aumentar la vasoconstricción pulmonar y agravar la hipoxemia; además, el frío puede reducir la producción de surfactante, empeorando la función respiratoria [15].

## Partes de la incubadora
Cubierta transparente (canopy): aísla al neonato, reduce las corrientes de aire y permite observarlo. Las cubiertas de una sola pared ofrecen menor aislamiento frente a la radiación térmica, y las aperturas prolongadas favorecen la pérdida de calor. En el proyecto se emplea acrílico con apertura y cierre.

Puertas de acceso (ojos de buey): permiten manipular al neonato sin abrir toda la cubierta, reduciendo las pérdidas térmicas.

Colchón o bandeja: soporta al neonato; una superficie fría aumenta la pérdida de calor por conducción. 

Calefactor (resistencia): transforma energía eléctrica en calor por efecto Joule. Una falla puede causar hipotermia, mientras que un funcionamiento continuo sin regulación puede provocar sobrecalentamiento.

Ventilador: distribuye el aire caliente por convección forzada. Su detención puede generar zonas con temperaturas desiguales y favorecer el sobrecalentamiento del calefactor.

Filtro de aire: reduce partículas y microorganismos transportados por el aire. 
Sensor de temperatura del aire: mide la variable controlada. Una lectura incorrecta puede provocar un calentamiento insuficiente o excesivo.

Sonda de piel: mide la temperatura cutánea del neonato para regular el calentamiento en modo servo.

Unidad de control: compara la temperatura medida con la consigna y regula el calefactor mediante estrategias como ON/OFF, PI o PID.

Alarmas y corte de seguridad: alertan sobre temperaturas anormales y fallas. Un termostato independiente puede interrumpir el calentamiento si falla el control principal. 

Humidificador: regula la humedad para reducir la pérdida de agua por la piel. Una humedad insuficiente favorece la deshidratación, mientras que una humedad elevada sin control puede aumentar el riesgo de contaminación.

Entrada de oxígeno: permite administrar oxígeno suplementario de forma controlada.

Báscula integrada: permite estimar el peso sin retirar al neonato.

Panel y alimentación: permiten visualizar temperatura, peso y alarmas. Una alimentación con respaldo ayuda a mantener el funcionamiento ante interrupciones eléctricas.

## Consecuencias de un ambiente no controlado o de fallas en la incubadora
### Temperatura baja (hipotermia). 
Se define generalmente como una temperatura corporal inferior a 36,5 °C en el neonato [7, 8]. Se asocia con hipoglucemia, acidosis metabólica, dificultad respiratoria, apnea, mayor riesgo de infección y alteraciones del crecimiento [14, 15]. En prematuros y neonatos de bajo peso también se relaciona con mayor mortalidad y complicaciones como síndrome de dificultad respiratoria, enterocolitis necrosante y hemorragia intraventricular [11]. Las fallas del calefactor o del ventilador y las aperturas prolongadas pueden favorecer su aparición.

### Temperatura alta (hipertermia).
Una temperatura superior a 37,5 °C suele considerarse elevada en el contexto neonatal [14], aunque su interpretación depende del sitio de medición y del contexto clínico. El exceso de calor favorece la deshidratación y puede alterar la frecuencia cardiaca y la respiración [9]. La asociación entre sobrecalentamiento y síndrome de muerte súbita del lactante se ha estudiado principalmente en lactantes mayores, por lo que no debe extrapolarse directamente a neonatos. En climas cálidos, el control térmico ambiental cobra especial importancia [5]. En el prototipo, una falla crítica sería que el calefactor permaneciera encendido sin regulación.

### Humedad baja.
La piel inmadura del prematuro pierde agua con facilidad, lo que puede provocar deshidratación, hipernatremia y pérdida de peso [10]. Además, la evaporación aumenta la pérdida de calor y puede contribuir a la hipotermia.

### Humedad alta.
Reduce la pérdida de agua, pero su uso prolongado puede favorecer la proliferación microbiana. Una revisión sistemática encontró una asociación entre niveles elevados de humedad y mayor riesgo de infección en prematuros (RR ≈ 1,26) [10]. Sus beneficios y riesgos dependen de la humedad, la duración y las condiciones clínicas; no existe un único nivel óptimo para todos los neonatos.

### Peso bajo. Se clasifica como bajo peso al nacer (< 2500 g), muy bajo peso (< 1500 g) y extremadamente bajo peso (< 1000 g) [11]. Se asocia con mayor riesgo de dificultad respiratoria, displasia broncopulmonar, hemorragia intraventricular, enterocolitis necrosante, retinopatía del prematuro, sepsis, hipoglucemia y dificultades de termorregulación [11]. La medición del peso dentro de la incubadora permite seguir el crecimiento y apoyar la evaluación nutricional y del balance de líquidos sin exponer al neonato a pérdidas térmicas por manipulación. Sin embargo, los cambios de peso deben interpretarse junto con la evaluación clínica, ya que no indican por sí solos deshidratación o sobrecarga de líquidos. Una báscula imprecisa puede conducir a decisiones clínicas incorrectas.

### Luz. La exposición excesiva o los cambios bruscos de iluminación pueden alterar el sueño y la estabilidad fisiológica del neonato. Los prematuros son especialmente sensibles a la luz, por lo que se recomienda una iluminación regulable y el uso de cubiertas cuando corresponda [13]. La fototerapia azul para tratar la ictericia es una intervención distinta que requiere protección ocular adecuada.

### Ruido. Se recomiendan niveles ambientales bajos en las unidades neonatales, con referencias de menos de 45 dB(A) y límites específicos para picos transitorios [12, 13]. Dentro de las incubadoras pueden registrarse niveles aproximados de 50–60 dB(A), en parte por el ventilador [12]. El ruido excesivo puede alterar la frecuencia cardiaca, la saturación de oxígeno y el sueño.

### Oxígeno y flujo de aire. La administración de oxígeno debe ajustarse y monitorizarse: una cantidad insuficiente puede causar hipoxemia, mientras que una exposición excesiva aumenta el riesgo de retinopatía del prematuro y displasia broncopulmonar. Las corrientes rápidas de aire junto al neonato incrementan la pérdida de calor; la detención del ventilador puede generar temperaturas desiguales y la ausencia de filtración adecuada puede aumentar el riesgo de contaminación.

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

#### 4. Sistema de medición del peso
Para estimar la masa de un objeto colocado sobre la plataforma se incorporó una galga o sensor de fuerza. Este elemento responde a la carga aplicada mediante una variación eléctrica que debe ser interpretada por el sistema de adquisición.

En el prototipo se realizaron pruebas con diferentes configuraciones de conexión, buscando obtener una lectura de peso más sensible. Sin embargo, debido a que los valores medidos presentaron diferencias respecto a las masas de referencia, el sistema no se consideró completamente calibrado.

Durante las pruebas, una masa de referencia de 1800 g produjo una lectura de 2305 g. El error absoluto fue de 505 g y el error porcentual, calculado respecto a la masa de referencia, fue del 28,06 %.

Este resultado evidencia la necesidad de mejorar la calibración y la adquisición de la señal del sensor para aumentar la exactitud de las mediciones.
#### 5. Interfaz de visualización mediante pantalla OLED
El prototipo incorpora una pantalla OLED para visualizar el valor de peso calculado por el sistema.

La pantalla se comunica con el Arduino Uno mediante las líneas SDA y SCL, correspondientes a los datos y al reloj del protocolo de comunicación.

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

## Análisis de Costos y Comparativa Comercial

### Tabla de Costos del Prototipo
| Componente / Elemento | Descripción / Especificación | Cantidad | Costo (COP) |
| :--- | :--- | :---: | :---: |
| **Tarjeta Arduino Uno R3** | Placa microcontroladora principal para adquisición | 1 | $40.000 |
| **Sensor DHT11** | Módulo sensor de temperatura y humedad relativa | 1 | $12.000 |
| **Galga de presión** | Celda de carga (1 kg / 5 kg) | 1 | $22.000 |
| **Pantalla OLED 0.96"** | Display I2C para visualización local de variables | 1 | $20.000 |
| **Elemento Calefactor (Bombillo + Socate)** | Fuente térmica incandescente para calefacción | 1 | $8.000 |
| **Módulo Relé (1 Canal / 5V)** | Conmutación del sistema de calefacción | 1 | $8.000 |
| **Ventilador DC (12V)** | Circulación de aire / convección térmica | 1 | $12.000 |
| **LEDs y Resistencias de Estado** | Indicadores ópticos (Rojo y Verde) y limitadores | 1 kit | $5.000 |
| **Estructura Físico-Mecánica** | Cabina a escala (44 cm x 20 cm x 22 cm) en madera | 1 | $65.000 |
| **Costo Total del Prototipo** | | | **$192.000** |

###  Comparativa con Soluciones Comerciales

* **Costo del Prototipo a Escala:** $192.000 COP ($48 USD).
* **Costo de Incubadora Comercial:** Rango aproximado entre **$15.000.000 COP y $60.000.000 COP** (~$3.800 - $15.000 USD) frente a marcas como Dräger, LEEX Medical e Instrumentalia S.A.S.

#### Principales Diferencias Técnicas y Funcionales

1. **Grado Médico y Certificación:** Los equipos comerciales incluyen servocontrol multivariable con algoritmos PI/PID, sistemas de redundancia de fallas, baterías de respaldo de grado hospitalario y homologaciones internacionales (ISO 13485 / FDA).
2. **Aislamiento y Materiales:** Las cabinas clínicas utilizan policarbonato de alta resistencia con aislamiento térmico optimizado y filtros HEPA para mantener entornos estériles.
3. **Sensores de Alta Calibración:** Los sensores comerciales poseen deriva térmica insignificante y tiempos de respuesta de milisegundos en comparación con módulos educativos como el DHT11.

# Parte C - Análisis y resultados






# Preguntas 
#### Pregunta 1: ¿Qué otras variables (y por qué) además de las aquí mencionadas son críticas en el monitoreo neonatal?
Además de la temperatura, la humedad relativa, el peso y el flujo de aire, las siguientes variables son importantes para la supervivencia y desarrollo del recién nacido:   
1. Concentración de Oxígeno: Es vital regular la inspiración de oxígeno para prevenir estados de hipoxia tisular o hiperoxia. Niveles descontrolados de oxígeno pueden desencadenar retinopatía de la prematuridad o daño pulmonar agudo.
2. Frecuencia Cardíaca y Respiratoria: El monitoreo electrocardiográfico o fotopletismográfico permite detectar de inmediato eventos críticos comunes en prematuros, como apneas, bradicardias o arritmias.
3. Saturación de Oxígeno: Evalúa en tiempo real la perfusión periférica y la efectividad de la ventilación.
4. Presión Arterial (No Invasiva e Invasiva): Es fundamental para evaluar el estado hemodinámico y prevenir estados de choque o hipotensión neonatal.
5. Nivel de Ruido e Iluminación: Niveles de ruido superiores a 45 dB o una luz ambiente intensa sobreestimulan el sistema nervioso inmaduro del prematuro, incrementando el consumo metabólico de oxígeno y alterando su neurodesarrollo.
#### Pregunta 2: ¿Qué haría falta para convertir el sistema desarrollado en una incubadora neonatal real?
Elevar los estándares de seguridad, precisión y estructura.   
1. Certificación Térmica y Eléctrica Médica (IEC 60601-2-19): Cumplimiento estricto de normativas internacionales de seguridad electromagnética, corrientes de fuga mínimas a tierra y aislamiento galvánico de alta protección.
2. Sensores de Grado Médico: Sustituir los módulos comerciales por sensores industriales de alta calibración y baja deriva térmica, implementando dos o más sondas de temperatura de piel y ambiente para evitar fallas por una lectura errónea.
3. Servocontrol Avanzado (PID): Reemplazar el control conmutado por algoritmos PID servocontrolados que ajusten la potencia del calefactor de forma proporcional y continua, garantizando variaciones térmicas inferiores a 0.1°C sin sobrepasos.
4. Cabina de Aislamiento Estéril y Filtros HEPA: Construir una estructura de doble pared de acrílico con grado óptico para reducir pérdidas por radiación, e integrar un sistema de circulación con filtros de aire HEPA que prevengan el ingreso de patógenos.
5. Sistemas de Seguridad, Alarmas y Batería de Respaldo: Implementar un sistema autónomo de alarmas audibles y visuales ante sobrecalentamiento 38°C, fallas de alimentación o detención del ventilador, acompañado de un sistema de alimentación ininterrumpida (UPS) de grado hospitalario.
#### Pregunta 3: ¿Qué semejanzas hay entre una incubadora neonatal y una servo-cuna?   
Tanto la incubadora neonatal como la servo-cuna comparten el objetivo fundamental de proporcionar soporte térmico para prevenir la hipotermia y reducir el estrés metabólico del recién nacido. Ambos sistemas funcionan bajo un principio de servocontrol en lazo cerrado mediante una sonda adherida a la piel del paciente, ajustando automáticamente la entrega de calor. Asimismo, incorporan monitoreo continuo de variables como la temperatura y el peso, y ofrecen un diseño que facilita la supervisión constante por parte del personal médico diferenciándose principalmente en que la incubadora es un entorno cerrado con control de humedad microambiental, mientras que la servo-cuna es una estructura abierta basada en calor radiante para acceso e intervenciones rápidas.
