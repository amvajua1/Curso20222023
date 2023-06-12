
# Web semántica y datos enlazados

Se presenta a continuación el índice seguido para el desarrollo de la práctica:


1. Introducción
2. Proceso de transformación:
	* Selección de la fuente de datos.
	* Análisis de los datos.
	* Estrategia de nombrado
	* Desarrollo del vocabulario.
	* Transformación de datos
	* Enlazado
	* Publicación.
3. Aplicación y explotación.
4. Conclusiones.
5. Bibliografía.


## 1. Introducción

En esta tarea se pide poner en práctica los conocimientos adquiridos a lo largo de la asignatura transformando un dataset en formato CSV de nuestra elección a datos enlazados.

Para ello, se ha seleccionado un dataset del portal de datos abiertos del Ayuntamiento de Santander que, con la ayuda de sensores distribuidos por la ciudad, recopilan datos relativos al nivel de ruido, luminosidad y temperatura.

## 2. Proceso de transformación

A lo largo de este apartado se llevarán a cabo cada una de las transformaciones necesarias para conseguir nuestro archivo RDF a partir de nuestro CSV de origen. 


### 2.1. Selección de la fuente de datos

Como se ha mencionado en el apartado de introducción, el CSV de origen, *Sensores ambientales*, se ha obtenido de la página del [portal de datos abiertos del Ayuntamiento de Santander](http://datos.santander.es/resource/?ds=sensores-ambientales&id=cae57038-c092-4743-b575-7bcafd838e02&ft=CSV).  


De entre toda la información a la que el ciudadano tiene acceso en dicho portal, he seleccionado este dataset en concreto para realizar la tarea debido a que me parece interesante la información recogida por los sensores ya que por ejemplo pueden ayudar a un ciudadano a encontrar la mejor zona para comprarse una vivienda en la ciudad. 


### 2.2. Análisis de los datos

El CSV seleccionado para la tarea tiene una licencia [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.es), es decir, podemos utilizar el dataset seleccionado para lo que deseemos, e incluso llegar a hacer modificaciones en el mismo siempre y cuando citemos al autor. Teniéndose esto en cuenta, se llevarán a cabo las transformaciones pertinentes manteniéndose la misma licencia para los datos transformados.


Se detallan a continuación cada una de las variables que componen el dataset:

| Columna | Tipo | Comentarios |
| ------------- | ------------- | -------------|
| dc:identifier | String | Identificador del registro
| dc:modified | String | Fecha y hora en que se tomó el registro expresada según el estándar ISO 8601
| ayto:type | String | Tipo de registro que el sensor va a medir. Toma dos valores posibles *NoiseLevelObserved* para las medidas del nivel de ruido y *WeatherLevelObserved* para las medidas de temperatura y nivel de luminosidad.
| ayto:latitude | String | Coordenadas de latitud que ubican al sensor
| ayto:longitude | String | Coordenadas de longitud que ubican al sensor
| ayto:temperature | String | Temperatura registrada por el sensor medida en grados Celsius. Solamente hay dato de este campo para el tipo *WeatherLevelObserved*. Presenta tres registros con temperaturas anómalas: 228.77 ºC, -39.09 ºC y -36.58ºC.
| ayto:battery | String | Nivel de batería del sensor medido en %. No presenta ningun valor para ningun registro
| ayto:light | String | Luminosidad registrada por el sensor medida en lúmenes. Solamente hay dato de este campo para el tipo *WeatherLevelObserved*. 
| ayto:noise | String | Nivel de ruido registrado por el sensor medido en dB. Solamente hay dato de este campo para el tipo *NoiseLevelObserved*.
| uri | String | URL que permite descargar un resumen de la información presente en el CSV para un registro concreto.


### 2.3. Estrategia de nombrado

Para seleccionar la estrategia de nombrado de los recursos haremos uso de # y /. Concretamente, utilizaremos el hash URIs (#) para los términos ontológicos y dado que el CSV seleccionado aporta información relativa a medidas recogidas por varios sensores, usaremos el slash URIs (/) para acceder a la información de cada una de las observaciones tal y como se describe a continuación:


* Dominio: http://ejemplo-sensores-ambientales.es/.
* Ruta para términos ontológicos: http://ejemplo-sensores-ambientales.es/ayto-santander/ontology/sensores#.
* Ruta para individuos: http://ejemplo-sensores-ambientales.es/ayto-santander/resource/ .


Teniendo esto en cuenta, los patrones para una propiedad y para un recurso específico de nuestro dataset serán:


* Patrón para términos ontológicos: http://ejemplo-sensores-ambientales.es/ayto-santander/ontology/sensores#hasTemperatura. 
* Patrón para individuos: http://ejemplo-sensores-ambientales.es/ayto-santander/resource/sensor/382.