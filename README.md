# Servicio-social
Este repositorio incluye mis trabajos para el servicio social en Aprendizaje de Máquina sobre el Impacto del Cambio en el Uso del Suelo sobre la Biodiversidad y el Bienestar.

Se sabe que el cambio climático es una realidad y que cada día existe una mayor variabilidad en las temperaturas. Por ello, es de suma importancia investigar este fenómeno desde distintas perspectivas. En este trabajo, se observa el cambio climático desde la década de 1850 hasta la actualidad, analizando los diferentes cambios que han ocurrido a lo largo de este tiempo y tratando de encontrar patrones al respecto.
![image](https://github.com/user-attachments/assets/b34b227c-902f-4cc9-9dbc-78cb8c225744)


# Espectros de Potencia
Propósito General

El objetivo del código es:

Dividir los datos en décadas: Para estudiar tendencias temporales y características específicas en intervalos regulares.
Calcular el espectro de potencia: Identificar las contribuciones de diferentes frecuencias en los datos medios de cada década.
Analizar pendientes en rangos de frecuencia específicos: Determinar cómo cambia la energía (potencia) en función de la frecuencia en dos rangos definidos.
Evaluar incertidumbres: Usar simulaciones aleatorias para calcular intervalos de confianza y visualizar la robustez de las pendientes y los espectros calculados.
Visualizar tendencias: Mostrar gráficamente cómo las pendientes y sus intervalos de confianza varían a lo largo de las décadas.
Utilizando los datos de Berkeley Earth Temperature, observamos la anomalía de la temperatura a lo largo del tiempo desde 1880. Vamos a dividir los datos en sus respectivas décadas, a las cuales les aplicaremos la transformada de Fourier para obtener su espectro de potencia.

Una vez teniendo esto, dividiremos este espectro en dos partes que nos interesa analizar: las series de tiempo cortas (0-30 días) y de medio alcance (30-180 días), para analizar las pendientes de estas y observar el cambio a lo largo de las décadas.

Para ello, primero descomponemos las señales de temperatura mediante la transformada de Fourier para obtener sus frecuencias. Luego, aplicamos el espectro de potencia, que mide la energía contenida en cada frecuencia de la señal, lo cual es útil para encontrar las frecuencias dominantes en los datos. Una vez hecho esto y seleccionados los rangos, calculamos las pendientes de la relación entre la frecuencia y el espectro de potencia en un gráfico log-log, obteniendo esta pendiente mediante un ajuste de regresión lineal.

Asimismo, para obtener intervalos de confianza, realizamos varias simulaciones aleatorias de los datos y nos quedamos con los percentiles (2.5% y 97.5%) para definir el intervalo de confianza.

![80c67924-f9d2-40c2-be7f-21dfb0ff9d82](https://github.com/user-attachments/assets/20431544-32ec-4b50-9aad-af303fa0d38e)

![3f90dc5d-e7b3-473a-9653-c8c48158a283](https://github.com/user-attachments/assets/f20a0fd5-f7b4-4447-841a-e2e0772f79ed)


Análisis de Comunidades a partir de la Temperatura
Utilizando los datos geográficos y de temperatura a lo largo de las décadas desde 1850, queremos ver cuáles son algunas comunidades que se forman y cómo han cambiado a lo largo del tiempo.

Primero, teniendo los datos de , interpolamos los datos vacíos bajo los siguientes criterios:

Para cada punto del mapa, calculamos su información mutua con todos los otros puntos para cada década (también se probó con correlación de Pearson, pero al no limitarse a variables en números reales ni a relaciones lineales, la información mutua es más general). Este proceso, al ser computacionalmente pesado, se realizó utilizando un clúster de computadoras.

Con estas matrices, procedemos a crear una red geográfica donde, si la información mutua entre cualquier par de nodos es mayor a 0.8 (con la intención de simplificar la red y enfocarnos en las relaciones más significativas), se crea una arista entre ellos. Una vez que tenemos nuestras redes, queremos detectar las comunidades para identificar agrupamientos de nodos fuertemente conectados entre sí. Para ello, utilizamos el método de Louvain, que ayuda a identificar las comunidades maximizando la modularidad—una medida de la calidad de las particiones en comunidades, donde valores altos indican comunidades bien definidas.

Como queremos ver el cambio a lo largo de las décadas, para cada década se crea una red. Sin embargo, el método de Louvain genera nuevas etiquetas para las comunidades en cada década, lo que implica que no se detectan las mismas comunidades en décadas distintas. Para solucionar esto, creamos una función que compara cada comunidad con las de la década anterior para encontrar las más similares en base a los nodos que las componen, aplicando así la misma etiqueta a las comunidades a lo largo del tiempo. Con esto, aplicamos métricas a las redes, observando la modularidad, el número de comunidades y cuántos nodos permanecen constantes a lo largo de las transiciones entre décadas.

Este código combina análisis de redes, teoría de la información y geografía para identificar y visualizar comunidades en redes espaciales basadas en información mutua. El uso de métricas, reetiquetado y visualización asegura que los resultados sean interpretables y comparables a lo largo del tiempo.

![community_maps_over_decades](https://github.com/user-attachments/assets/97addee6-f3da-46e1-85c1-e320cb117053)
Se puede observar que como es intuitivo las comunidades estan dadas por cercania geográfica, ademas de que, divisiones de la tierra clara como es el caso de la costa maritima suelen dividir a las comunidades. Así mismo existen varias comunidades que suelen ser bastantes constantes a lo loargo de las décadas.
![community_bar_charts_over_decades](https://github.com/user-attachments/assets/7f5fdb73-f830-4331-ada5-92741f7fe150)



# DMD (Dinamic model descompsition)
Se inició la implementación de la técnica de Descomposición de Modelos Dinámicos (DMD) y Análisis de Componentes Principales (PCA) para analizar los datos y obtener información sobre la evolución temporal de los diferentes componentes del sistema, con el fin de identificar sus componentes fundamentales. Aunque no se obtuvieron resultados relevantes con estos métodos, a continuación, comparto un resumen del proceso seguido. 

El enfoque se centró en zonas geográficas específicas, como distintas corrientes marinas. El objetivo era analizar cómo cambia la temperatura a lo largo del tiempo y el espacio. Para ello, se utilizó DMD para descomponer las variaciones dinámicas de los datos y generar una reconstrucción que permitiera un análisis más simplificado de estos comportamientos complejos. De esta forma, se trató de entender los componentes fundamentales del sistema, como oscilaciones, tendencias o patrones recurrentes, al evaluar los modos dinámicos que dominan el comportamiento de las corrientes y cómo contribuyen a la variabilidad de la temperatura. Esto tenía como objetivo realizar predicciones y pronósticos sobre el futuro del sistema. 

Lamentablemente, no se logró obtener reconstrucciones que fueran fieles a la realidad, ya que este método matemático requiere de datos muy limpios y sin ruido, algo que no fue posible debido a la forma en que se obtuvieron los datos. Por este motivo, se abandonó esta línea de investigación para concentrarnos en las actividades previamente mencionadas. 
