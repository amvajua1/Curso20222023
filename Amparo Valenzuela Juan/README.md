# Certificaciones energéticas de edificios

1. Introducción
2. Proceso de transformación:
    * 2.1 Selección de la fuente de datos
    * 2.2 Análisis de los datos
    * 2.3 Estrategia de nombrado
    * 2.4 Desarrollo del vocabulario
    * 2.5 Transformación de datos
    * 2.6 Enlazado
    * 2.7 Publicación

4. Aplicación y explotación
5. Conclusiones
6. Bibliografía

## 1. Introducción

Del catálogo de datos publicado en _[Datos Gobierno de España](https://datos.gob.es/es/sector/medio-ambiente)_, se ha escogido un conjunto de datos en el ámbito del medio ambiente, en el que se informa sobre las certificaciones energéticas de un edificio. El objetivo de este documento es describir la transformación de dicho conjunto de datos con formato csv en datos enlazados, aplicando las metodologías más apropiadas, con el fin de aportar valor al usuario final. De forma que, toda la información enlazada sobre el registro de certificados de eficiencia energética de edificios le sea útil al comprador o usuario a la hora de comprar o alquilar un edificio o vivienda.

## 2. Proceso de transformación

Para llevar a cabo el proceso de transformación de los datos en formato csv a datos enlazados, primero se realiza una selección de la fuente de datos descrito en el aprtado 2.1, de dichos datos un análisis de los mismos: tipos, formato etc, desarrollado en el punto 2.2. En el apartado 2.3 se explica la estrategia de nombrado, cómo se van a nombrar los recursos del vocabulario y datos, y su desarrollo se comenta en el apartado 2.4. En el punto 2.5 se lleva a cabo la transformación de los datos, y su enlazado se explica en el punto 2.6. Por último, su publicación se describe en el apartado 2.7.

### 2.1. Selección de la fuente de datos

Los datos seleccionados se han descargado de la web _[Iniciativa de datos abiertos del Gobierno de España](https://datos.gob.es)_, se trata de una web del gobierno de España, del ministerio de asuntos económicos y transformación digital para la reutilización de información pública. Concretamente se han descargado del catálogo de datos, el conjunto de datos _[Certificaciones energéticas](https://datos.gob.es/es/catalogo/a15002917-certificaciones-energeticas)_. El publicador de los datos es la [Comunidad Foral de Navarra](https://datos.gob.es/es/catalogo?publisher_display_name=Comunidad+Foral+de+Navarra). El por qué de la selección de dichos datos, ha sido por el hecho de ser información muy útil para el usuario a la hora de comprar o alquilar una vivienda y porque cumplen los requisios para su selección: escenario real, datos disponibles, formato procesable automáticamente e csv y posibilidad de enlazar con entidades genéricas.

De acuerdo con la página web citada, se describen los datos como:

La certificación de eficiencia energética de un edificio es el proceso por el cual se obtiene la calificación de eficiencia energética del edificio, calificación que permite valorar el consumo de energía del edificio y  las emisiones de gases de efecto invernadero asociadas a dicho consumo energía. Esta calificación se expresa gráficamente mediante una etiqueta de eficiencia energética, similar a la de los electrodomésticos, que       
asigna a cada edificio una clase energética de eficiencia, que va desde la clase A, para los edificios de menor consumo energético, a la clase G, para los menos eficientes. El Registro de certificados de eficiencia 
energética de edificios ofrece información de las características energéticas de los edificios, para que los compradores y usuarios la tengan en cuenta a la hora de comprar o alquilar un edificio o vivienda.


### 2.2. Análisis de los datos

La licencia de los datos escogidos proviene de [Creative Commons Attribution License (cc-by)](http://www.opendefinition.org/licenses/cc-by), ésta permite la redistribución y la reutilización de una obra con licencia con la condición de que se acredite debidamente al creador. La licencia que utilizan es [CC-BY](https://creativecommons.org/choose/) con reconocimiento 4.0 internacional, de cultura libre, que permite compartir las adaptaciones de la obra y que permite usos comerciales. Por las características propias de la licencia, se utilizará la misma para los datos transformados. 

La frecuencia de actualización de los datos es diaria, por lo que en la descarga del fichero con fecha 14/06/2023, tiene una totalidad del 78.511 filas. En la siguiente tabla se detalla el análisis de las características de los datos:

|Nombre campo|	Tipo dato |Descripción|Características|                  
| --- | --- | --- | --- |
|_id|numeric|identificador del registro|pk, valor no nulo|
|CodEdificio|string|código edificio|único, valor no nulo|
|Tipo|string|tipo de edificación: nuevo, existente, terminado, proyecto|valor no nulo; valores:existente, terminado, proyecto, reformado|
|CodRegistroComAutonoma|string|código registro de la comunidad autónoma|valor no nulo|
|Direccion|string|dirección del edificio|valor no nulo|
|Localidad|string|localidad del edificio|no hay datos|
|CP|string|código postal del edificio|contiene vacíos|
|Provincia|string|provincia del edificio|no hay datos|
|Zona|string|zona del edificio|contiene vacíos|
|AnioConstruccion|integer|anyo de construcción del edificio|contiene vacíos, datos en string, y anyos ilógicos|
|NormativaVigente|string|normativa vigente|contiene vacíos, datos ilógicos|
|ReferenciaCatastral|string|referencia catastral|contiene vacíos|
|TipoDeEdificio|string|tipo del edificio|contiene vacíos, datos con valor -1|
|Procedimiento|string|procedimiento certificación|contiene vacíos|
|Fecha|date|fecha edificación|contiene vacíos|
|SuperficieHabitable|numeric|superficie habitable de la vivienda|no hay datos|
|PorcentajeSuperficieHabitableCalefactada|numeric|porcentaje de superficie habitada con calefacción|no hay datos|
|PorcentajeSuperficieHabitableRefrigerada|numeric|porcentaje de superficie habitada con aire acondicionado|no hay datos|
|PorcentajeSuperficieHabitableAcristalada|numeric|porcentaje de superficie habitada acristalada|no hay datos|
|DemandaDiariaACS|numeric|demanda diaria ACS (agua caliente sanitaria)|no hay datos|
|GeneradoresCalefaccion|string|generadores de calefacción|contiene vacíos; conjunto datos clasificados con Nombre: ;Tipo: ; Pot.Nominal: 0; RendimientoEst.: 0; Vec.Energetico: ; ModoObtencion:|
|GeneradoresRefrigeracion|string|generadores de refigeración|contiene vacíos;conjunto datos clasificados con Nombre: ;Tipo: ; Pot.Nominal: 0; RendimientoEst.: 0; Vec.Energetico: ; ModoObtencion:|
|InstalacionesACS|string|instalaciones ACS (agua caliente sanitaria)|contiene vacíos;conjunto datos clasificados con Nombre: ;Tipo: ; Pot.Nominal: 0; RendimientoEst.: 0; Vec.Energetico: ; ModoObtencion:|
|SistemasTermicos|string|sistemas térmicos|contiene vacíos; conjunto datos clasificados con Nombre: ;Cons.Fin.Calefaccion: ; Cons.Fin.Refrigeracion: ; Cons.Fin.ACS.: ; DemandaACS: |
|SistemasElectricos|string|sistemas eléctricos|contiene vacíos; conjunto datos clasificados con Nombre: ;Ener.Gen.Autoconsumida:|
|PotenciaTotalInstalada|decimal|potencia total instalada|contiene vacíos; valores positivos|
|Nombre|string|nombre de la contribución energética|contiene vacíos|
|ConsumoFinalCalefaccion|decimal|consumo final de la calefacción|contiene vacíos; valores positivos|
|ConsumoFinalRefrigeracion|decimal|consumo final de refigeración|contiene vacíos; valores positivos|
|ConsumoFinalACS|decimal|consumo final ACS (agua caliente sanitaria)|contiene vacíos; valores positivos|
|DemandaACS|decimal|demanda ACS (agua caliente sanitaria)|contiene vacíos; valores positivos|
|Nombre1|string|nombre de la contribución energética|contiene vacíos|
|EnergiaGeneradaAutoconsumida|decimal|energía general de autoconsumo|contiene vacíos; valores positivos|
|ReduccionGlobalEnergiaPrimariaNoRenovable|decimal|reducción global de energía primaria no renovable|contiene vacíos; valores positivos|
|Global|numeric|en general|no hay datos|
|Calefaccion|numeric|calefacción|no hay datos|
|Refrigeracion|numeric|refrigeración|no hay datos|
|ACS|numeric|ACS (agua caliente sanitaria)|no hay datos|
|GasNatural|string|gas natural|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|GasoleoC|string|gasoleo|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|GLP|string|GLP (gas licuado de petróleo) combustión limpia|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|Carbon|string|carbón|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|BiomasaPellet|string|biomasa pellet|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|BiomasaOtros|string|biomasa otros|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|ElectricidadPeninsular|string|electricidad en la Península|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|ElectricidadBaleares|string|electicidad en Baleares|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|ElectricidadCanarias|string|electricidad en Canarias|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|ElectricidadCeutayMelilla|string|electricidad en Ceuta y Melilla|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|Biocarburante|string|biocarburante|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|EnergiaPrimNoRenovable|string|energía prima no renovable|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación:|
|EmisionesCO2|string|emisiones CO2|contiene vacíos; conjunto datos clasificados con Global: ;Calefacción: ;Refrigeración: ;ACS: ;Iluminación: ;Cons.Eléctrico:;Cons.Otros:;Tot.Cons.Electrico:;Tot.Cons.Otros: |
|CalificacionDemandaEscalaCalefaccion|string|calificación de la demanda en escala de la calefacción|contiene vacíos;conjunto datos clasificados con A:;B:;C: ;D: ;E: ;F:|
|CalificacionDemandaEscalaRefrigeracion|string|calificación de la demanda en escala de la refrigeración|contiene vacíos;conjunto datos clasificados con A:;B:;C: ;D: ;E: ;F:|
|CalificacionDemandaCalefaccion|string|calificación demanda calefacción|contiene vacíos; char(1)|
|CalificacionDemandaRefrigeracion|string|calificación demanda refrigeración|contiene vacíos; char(1)|
|CalificacionEnePrinNoRenovEscalaGlobal|string|calificación energia principal no renovable en escala global|contiene vacíos;conjunto datos clasificados con A:;B:;C: ;D: ;E: ;F:|
|CalificacionEnePrinNoRenovGlobal|string|calificación energia principal no renovable global|contiene vacíos; char(1)|
|CalificacionEnePrinNoRenovCalefaccion|string|calificación energia principal no renovable en calefaccion|contiene vacíos; char(1)|
|CalificacionEnePrinNoRenovRefrigeracion|string|calificación energia principal no renovable en refrigeración|contiene vacíos; char(1)|
|CalificacionEnePrinNoRenovACS|string|calificación energia principal no renovable en ACS|contiene vacíos; char(1)|
|CalificacionEnePrinNoRenovIluminacion|string|calificación energia principal no renovable en iluminación|contiene vacíos; char(1)|
|CalificacionEmiCO2EscalaGlobal|string|calificación en emisiones CO2 en escala global|contiene vacíos;conjunto datos clasificados con A:;B:;C: ;D: ;E: ;F:|
|CalificacionEmiCO2Global|string|calificación en emisiones CO2 global|contiene vacíos; char(1)|
|CalificacionEmiCO2Calefaccion|string|calificación en emisiones CO2 en calefacción|contiene vacíos;char(1)|
|CalificacionEmiCO2Refrigeracion|string|calificación en emisiones CO2 en refrigeración|contiene vacíos; char(1)|
|CalificacionEmiCO2ACS|string|calificación en emisiones CO2 en ACS|contiene vacíos;un char(1)|
|CalificacionEmiCO2Iluminacion|string|calificación en emisiones CO2 en iluminación|contiene vacíos; char(1)|



### 2.3. Estrategia de nombrado



### 2.4. Desarrollo del vocabulario



### 2.5. Transformación de datos


### 2.6. Enlazado


