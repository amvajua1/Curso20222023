# **_Certificación energética de edificios_**

1. Introducción
2. Proceso de transformación:
    * 2.1 Selección de la fuente de datos
    * 2.2 Análisis de los datos
    * 2.3 Estrategia de nombrado
    * 2.4 Desarrollo del vocabulario
    * 2.5 Transformación de datos
    * 2.6 Enlazado
    * 2.7 Publicación

3. Aplicación y explotación
4. Conclusiones
5. Bibliografía

## 1. Introducción

Del catálogo de datos publicado en _[Datos Gobierno de España](https://datos.gob.es/es/sector/medio-ambiente)_, se ha escogido un conjunto de datos en el ámbito del medio ambiente, en el que se informa sobre las certificaciones energéticas de un edificio. El objetivo de este documento es describir la transformación de dicho conjunto de datos con formato csv en datos enlazados, aplicando las metodologías más apropiadas, con el fin de aportar valor al usuario final. De forma que, toda la información enlazada sobre el registro de certificados de eficiencia energética de edificios le sea útil al comprador o usuario a la hora de comprar o alquilar un edificio o vivienda.

## 2. Proceso de transformación

Para llevar a cabo el proceso de transformación de los datos en formato csv a datos enlazados, primero se realiza una selección de la fuente de datos descrito en el aprtado 2.1, de dichos datos un análisis de los mismos: tipos, formato etc, desarrollado en el punto 2.2. En el apartado 2.3 se explica la estrategia de nombrado, cómo se van a nombrar los recursos del vocabulario y datos, y su desarrollo se comenta en el apartado 2.4. En el punto 2.5 se lleva a cabo la transformación de los datos, y su enlazado se explica en el punto 2.6. Por último, su publicación se describe en el apartado 2.7.

### 2.1. Selección de la fuente de datos

Los datos seleccionados se han descargado de la web _[Iniciativa de datos abiertos del Gobierno de España](https://datos.gob.es)_, se trata de una web del gobierno de España, del ministerio de asuntos económicos y transformación digital para la reutilización de información pública. Concretamente se han descargado del catálogo de datos, el conjunto de datos _[Certificaciones energéticas](https://datos.gob.es/es/catalogo/a15002917-certificaciones-energeticas)_. El publicador de los datos es la [Comunidad Foral de Navarra](https://datos.gob.es/es/catalogo?publisher_display_name=Comunidad+Foral+de+Navarra). El por qué de la selección de dichos datos, ha sido por el hecho de ser información muy útil para el usuario a la hora de comprar o alquilar una vivienda y porque cumplen los requisios para su selección: escenario real, datos disponibles, formato procesable automáticamente en csv y posibilidad de enlazar con entidades genéricas.

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
|Zona|string|zona climática del edificio|contiene vacíos|
|AnioConstruccion|integer|anyo de construcción del edificio|contiene vacíos, datos en string, y anyos ilógicos|
|NormativaVigente|string|normativa vigentenormativa vigente (construcción/rehabilitación)|contiene vacíos, datos ilógicos|
|ReferenciaCatastral|string|referencia catastral|contiene vacíos|
|TipoDeEdificio|string|tipo del vivienda|contiene vacíos, datos con valor -1|
|Procedimiento|string|procedimiento reconocido de calificación energética utilizado y versión|contiene vacíos|
|Fecha|date|fecha realizada certificación energética del edificio|contiene vacíos|
|SuperficieHabitable|numeric|superficie habitable de la vivienda|no hay datos|
|PorcentajeSuperficieHabitableCalefactada|numeric|porcentaje de superficie habitada con calefacción|no hay datos|
|PorcentajeSuperficieHabitableRefrigerada|numeric|porcentaje de superficie habitada con aire acondicionado|no hay datos|
|PorcentajeSuperficieHabitableAcristalada|numeric|porcentaje de superficie habitada acristalada|no hay datos|
|DemandaDiariaACS|numeric|demanda diaria ACS (agua caliente sanitaria)|no hay datos|
|GeneradoresCalefaccion|string|generadores de calefacción|contiene vacíos; característica energética del edificio con Nombre: ;Tipo: ; Pot.Nominal: 0; RendimientoEst.: 0; Vec.Energetico: ; ModoObtencion:|
|GeneradoresRefrigeracion|string|generadores de refigeración|contiene vacíos;característica energética del edificio con Nombre: ;Tipo: ; Pot.Nominal: 0; RendimientoEst.: 0; Vec.Energetico: ; ModoObtencion:|
|InstalacionesACS|string|instalaciones ACS (agua caliente sanitaria)|contiene vacíos;característica energética del edificio con Nombre: ;Tipo: ; Pot.Nominal: 0; RendimientoEst.: 0; Vec.Energetico: ; ModoObtencion:|
|SistemasTermicos|string|sistemas térmicos|contiene vacíos; característica energética del edificio con Nombre: ;Cons.Fin.Calefaccion: ; Cons.Fin.Refrigeracion: ; Cons.Fin.ACS.: ; DemandaACS: |
|SistemasElectricos|string|sistemas eléctricos|contiene vacíos; característica energética del edificio con Nombre: ;Ener.Gen.Autoconsumida:|
|PotenciaTotalInstalada|decimal|potencia total instalada|contiene vacíos; valores positivos|
|Nombre|string|nombre sistema térmico|contiene vacíos|
|ConsumoFinalCalefaccion|decimal|consumo final de la calefacción|contiene vacíos; valores positivos|
|ConsumoFinalRefrigeracion|decimal|consumo final de refigeración|contiene vacíos; valores positivos|
|ConsumoFinalACS|decimal|consumo final ACS (agua caliente sanitaria)|contiene vacíos; valores positivos|
|DemandaACS|decimal|demanda ACS (agua caliente sanitaria)|contiene vacíos; valores positivos|
|Nombre1|string|nombre sistema eléctrico|contiene vacíos|
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
|ElectricidadBaleares|string|electicidad en Baleares|no hay datos|
|ElectricidadCanarias|string|electricidad en Canarias|no hay datos|
|ElectricidadCeutayMelilla|string|electricidad en Ceuta y Melilla|no hay datos|
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

Se define la estragia de nombrado tanto para recursos Web como entidades fuera de la Web. Son clave en los datos enlazados y se identifican mediante URIs persistentes. A continuación se define la estrategia de nombrado de recursos:

* Elección de la forma de las URIs:
  - Se utiliza el símbolo hash '#' para la redirección a un documento, con acceso completo a los datos. Y el símbolo slash '/' para la identificación de recursos que son dinámicos.
* Elección del dominio de las URIs:
  - Dominio: http//CEE.es/ 
* Elección ruta de las URIs:
  - Ruta para términos ontológicos: http//CEE.es/datosgob/ontology/CertificacionEnergeticaCEE#
  - Ruta para individuos: http//CEE.es/datosgob/resource/
* Elección patrones para clases, propiedades e individuos:
  - Patrón para términos ontológicos: http//CEE.es/datosgob/ontology/CertificacionEnergeticaCEE#<term_name>
  - Patrón para individuos: http//CEE.es/datosgob/resource/<resource_name>

### 2.4. Desarrollo del vocabulario

El desarrollo ontológico a tratar sigue la metodología de NeOn, pero sin hacerla demasiado extensa. En primer lugar se define la especificación de requisitos que satisface los requisitos no funcionales y funcionales:
* Especificación de requisitos:
   - Requisitos no funcionales:
      - El idioma de la ontología deberá ser en inglés por ser idioma universal, y en español por enfocarse la ontología en la certificación energética en España.
      - Escalable, de forma que podrá incorporar nueva información relacionada con la certificación energética en edificios, tales como: nuevas normativas en la certificación, nuevas califaciones o procedimientos.
   - Requisitos funcionales:
      - Se refieren al conocimiento que debe representar la ontología, que haciendo uso de la metodología de NeOn, se basa en Preguntas por Competencia (PC):
        
      |Identificador|Pregunta Competecia|Posible respuestas|                  
      | --- | --- | --- |
      |PC1|¿Identificación del edificio?|Nombre, dirección, municipio, zona climática, normativa vigente, referencia catastral, CP, anyo construcción, tipo de edificio|
      |PC2|¿Datos técnicos certificación energética?|procedimiento reconocido de calificación energética, fecha certificación energética del edificio|
      |PC3|¿Características energéticas del edificio?|instalaciones térmicas (generadores de calefacción y refrigeración), instalaciones ACS, energía térmica y eléctrica|
      |PC3|¿Calificación energética?|Cal.Obtenida, Cal.Emisiones, Cal.Consumo, Cal.Parcial demanda, Cal.Global, Cal.Parcial|
      |PC4|¿Tipo energía edificio?|carbón, biomasa, electricidad Peninsular, biomasa pellet, GLP|
      |PC5|¿Consumo energético?|Global: 193.00;Calefacción: 150.38;Refrigeración: 0.00;ACS: ;Iluminación: 0.00|
      
* Extracción de términos:
   - Se extrae terminología relacionada con la certificación energética en edificios para su mejor entendimiento:  

      |Término|Concepto|                 
      | --- | --- |
      |Indicador Global de Emisiones|Es la letra o calificación del inmueble (letras entre D y E).|
      |Instalación térmica|Para producción de agua caliente y producción de calefacción o frío.|
      |Calificación Energética del Edificio|Se expresa en términos de dióxido de carbono liberado a la atmósfera como consecuencia del consumo energético del mismo.|
      |Calificación Parcial del Consumo de Energía Primaria|Energía consumida por el edificio procedente de fuentes renovables y no renovables que no ha sufrido ningún proceso de conversión o transformación.|
      |Calificación energética A|Muy alto nivel de eficiencia, consumo energético 55% inferior a la media.|
      |Calificación energética B|Consumo energético entre 55% y 75%.|
      |Calificación energética C|Consumo energético entre 75% y 90%.|
      |Calificación energética D|Consumo energético entre 90% y 100%.|
      |Calificación energética E|Consumo energético entre 100% y 110%.|
      |Calificación energética F|Consumo energético entre 110% y 125%.|
      |IPE|Consumo global de energía primaria. Se mide en Kw/m2*año.|
      |kWh/m2|Indica la cantidad de energía que es necesario consumir para vivir en esa casa de forma confortable.|
      |Kg de CO2|La energía, aunque no provenga de la quema de combustibles, conlleva una emisión de gases y contaminantes. Por cada kilo de combustible se emite un número determinado de kilos de CO2, lo mismo pasa con la generación de la electricidad, por cada kWh se emiten un número de gramos de CO2.| 
         
* Conceptualización:
  - A continuación se muestra un primer mapa conceptual que representa los principales conceptos que deberá tener la ontología, que describe el dominio de certificación energética de edificios denominado como CEE.
    Para llevarlo a cabo, se ha tenido en cuenta las preguntas de competencia y la especificación de requisitos detallados en los apartados anteriores:

     <img width="390" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/3610b7ff-ef59-45d6-9571-bca54dd9e634">

  - Dominios y conceptos clave:

     |Entidad|Atributo|Relación                 
     | --- | --- |--- |
     |CertificacionEnergetica|procedimiento, fechaCertif|- Una certicación energética pertenece a un edificio (perteneceEdificio)|
     |Edificio|codEdificio, tipo, codRegistroComAutonoma, direccion, cp, zonaClimatica, anyoConstruccio, normativaVigente, referenciaCatastral, tipoEdificio|- Un edificio tiene características energéticas (tieneCaracEnergeticas). - Un edificio tiene certificación energética (tieneCertificacion).|
     |Caracteristicas|- Es clase de las subclases: Energia, Instalacion.|- Una característica energética tiene un tipo de energía (tieneTipoenergia)|
     |Energia|nombre, tipo, descripción|- Una característica energética tiene un tipo de energía (tieneTipoenergia)|
     |Instalacion|nombre, tipo, descripción|- Una característica energética tiene un tipo de energía (tieneTipoenergia)| 
     |TipoEnergia|tipo|- Un tipo de energía tiene consumo (tieneConsumo).|
     |Consumo|nombre, consumo|- Un consumo de un tipo de energía tiene calificación (tieneCalificacion).|  
     |Calificacion|- Es clase de las subclases: CalificaEnePrinNoRenov, CalificaEnergia, CalificaDemanad, CalificaEmiCO2.|- Una calificación energética pertenece a una certificación energética del edificio (perteneceCertificacion).|
     |CalificaEnePrinNoRenov|nombre, escala, calEnePrinNoRenovACS, calEnePrinNoRenovCalefaccion, calEnePrinNoRenovGlobal, calEnePrinNoRenovIluminacion, calEnePrinNoRenovRefrigeracion|- Una calificación energética pertenece a una certificación energética del edificio (perteneceCertificacion).|
     |CalificaDemanda|nombre, escala, calDemandaCalefaccion, calDemandaRefrigeracion|- Una calificación energética pertenece a una certificación energética del edificio (perteneceCertificacion).|
     |CalificaEmiCO2|nombre, escala, calEmiCO2Iluminacion, calEmiCO2ACS, calEmiCO2Refrigeracion, calEmiCO2Calefaccion, calEmiCO2Global|- Una calificación energética pertenece a una certificación energética del edificio (perteneceCertificacion).|
     |CalificaEnergetica|nombre, energiaPrimNoRenov, emisionesCO2|- Una calificación energética pertenece a una certificación energética del edificio (perteneceCertificacion).|

* Búsqueda de ontologías:
   - Para el dominio de certificaciones energéticas, se realizó una búsqueda exhaustiva de recursos que se están utilizando en la Linked Data Cloud, en el repositorio [LOV](https://lov.linkeddata.es/dataset/lov/vocabs). Se realizó una búsqueda de los siguientes
   términos: certificate, energy, building, qualification. Se encontraron las siguientes ontologías que posteriormente se analizaron: bot, saref, dco, esco.

* Ontologías encontradas en el repositorio [LOV](https://lov.linkeddata.es/dataset/lov/vocabs):
   - [Building Topology Ontology (bot)](https://w3c-lbd-cg.github.io/bot/): Es una ontología para describir los conceptos topológicos centrales de un edificio.
   - [SAREF extension for building (saref4bldg)](https://saref.etsi.org/saref4bldg/v1.1.2/#s4bldg:HeatExchanger): Esta ontología amplía la ontología SAREF para el dominio de la construcción al definir los dispositivos de construcción y cómo se ubican en un edificio.
   - [European Skills, Competences, qualifications and Occupations (esco)](https://ec.europa.eu/esco/lod/static/model.html): La ontología de la taxonomía "Habilidades, competencias, cualificaciones y ocupaciones europeas". La ontología considera tres pilares ESCO (o taxonomía) y 2 registros. Los tres pilares son: - Ocupación - Habilidad (y competencias) - Cualificación
   - [Ontology dco](https://www.dco.domos-project.eu/#crossreference): Ontología que define dispositivos en diferentes entornos.

* Selección de las ontologías de dominio:
   - La ontología _bot_ define el area por zonas de un edificio, por lo que se decide no reutilizarla. La ontología _SAREF_ sí que se encuentran entidades de características energéticas como el generador eléctrico, como objetos físicos o dispositivos en un edificio, pero se centra en la definición más que en el consumo. La ontología _esco_ no tiene ninguna entidad que se ajuste para ser reutilizada y la ontología _dco_ tiene clases muy interesantes como Gas, Gas boiler, pero tras cargar la ontología en Protégé y verla con detalle, no se ha visto la necesidad de su reutilización:

     <img width="175" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/90ae79d5-9b80-4d00-9aa3-3a19e12ac252">
     
* Implementación de la ontología:
  - Para la implementación de la ontología en el dominio de certificación energéticas de un edificio se ha utilizado la herramienta [Protégé versión 5.6.1](https://protege.stanford.edu/software.php), desarrollada por el grupo Stanford Medical Informatics de la universidad de Stanford en colaboración con la Universidad de Manchester.
  - La ontología se ha guardado como _ontoCEE_, y la siguiente imagen muestra el gráfico de la misma, diseñada desde del tab OntoGraf:
    <img width="488" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/91f65ccc-1f68-4d60-8a87-64200a21a72a">
    
  - Taxonomía. La jerarquía de las clases en la ontología se visualiza en la siguiente imagen:
    
    <img width="170" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/be885b9f-02a4-4793-aa57-f89c6dff2318">

* Evaluación de la ontología:
  - Se evalúa la ontología con la aplicación [OOPS!](https://oops.linkeddata.es/) haciendo Scanner by RDF, y el resultado es el siguiente:
    <img width="455" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/3bc4b969-9064-4e09-bd3c-5c315bd201ea">
  - Se re-evalúa la ontología y se resuelven gran parte de los pitfalls:

    <img width="623" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/8ad390e4-c02c-49bf-ac63-323d3bdfc921">

  -  El error _P41:No license declared_ persiste. Se investiga cómo resolverlo, y se encuentra la solución que consiste en declarar una anotación con dcterms:license, pero tras probarlo, el problema persiste en OOPS!. Se validan otras ontologías con OOPS! tales como dogont.rdf y persoon.rdf, pero también aparece el P41 pese a tener las anotaciones de licencia, por lo que se decide crear una [issue](https://github.com/AEPIA-WebSemanticaDatosEnlazados/Curso20222023/issues/13) en Github para comentarlo con el resto de usuarios y compartir el problema.
    
    <img width="476" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/2c52f060-7094-4718-addb-9e90f90cc982">

  -  El pitfall P22 tiene importancia baja y no es necesario resolverlo, por lo que se da como válido.
    
### 2.5. Transformación de datos
Se va a transformar la fuente de datos escogida y analizada en los apartados anteriores en formato _RDF_. La serialización elegida para RDF es _RDF-XML_ y la herramienta a utilizar para dar soporte a la transformación es [_OpenRefine_](https://openrefine.org/docs/manual/expressions#grel-general-refine-expression-language):
- Se cargan los datos:
<img width="957" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/d4fc45d5-3ef9-444e-8997-c8ad84725f3f">

- Se transforman la columna  _CP_, _AnioConstruccion_ que está como texto y es numérico:
<img width="644" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/0250beb3-d676-4c3c-90c9-634590311a60">

- Se eliminan las columnas que no tienen valor: _Localidad, SuperficieHabitable, PorcentajeSuperficieHabitableCalefactada,  PorcentajeSuperficieHabitableRefrigerada, PorcentajeSuperficieHabitableAcristalada, DemandaDiariaACS, ReduccionGlobalEnergiaPrimariaNoRenovable, Global, Calefaccion, Refrigeracion, ACS, ElectricidadBaleares, ElectricidadCanarias, ElectricidadCeutayMelilla_ 

- Se eliminan las columna que no se va a informar: _id
- Como los datos son de la provincia de _Navarra_, se añade manualmente el valor de la columna _Provincia_ que no tiene datos.
- Existen columnas con datos anidadados como _GeneradoresCalefaccion_ pero no se va hacer un Split sobre ellas ya que hay mucha informacion y se interpreta como descripción del recurso.
- Se renombran las columnas _Nombre_ por _NombreSistemaTermico_ y _Nombre1_ por _NombreSistemaElectrico_.
- Se cambia a numérico las siguientes columnas: _PotenciaTotalInstalada, ConsumoFinalCalefaccion, ConsumoFinalRefrigeracion, ConsumoFinalACS, DemandaACS, EnergiaGeneradaAutoconsumida_.
- Se eliminan las filas que tienen datos incompletos y no son coherentes. Para obtener las filas, se hace un facet sobre las columnas de calificación energética que no pueden estar vacías. En total tras realizar la limpieza de datos, se ha quedado con un total de 6010 filas de 78.511 registros que se habían cargado inicialmente, quedando fuera 72.510 con datos inconsistentes:
  
  <img width="953" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/d9a7e1e3-00bb-422f-a035-7772798e57cf">
- Se tienen problemas a la hora de codificar los caracteres 'ñ' y acentos, por lo que en una primera instancia se tratan desde 'Custom text transform on colum...' y se utiliza la expresión value.reinterpret('UTF-8','ISO-8859-1') entre diferentes combinaciones pero sin éxito. Finalmente se soluciona exportando los datos, codificando a ANSI desde Notepad y volviendo a importar los datos para continuar con su transformación, quedando de la siguiente forma (se adjunta proyecto en la carpeta ProyectoOpenRefine):

<img width="947" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/55742fba-2038-47b7-ad57-f0ae39925d58">

- También es posible la codificación al crear el proyecto en _OpenRefine_:

<img width="396" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/42bb29a5-6bb5-4bfa-aa3e-fe67846d8a38">

- Extensión RDF utilizada en _OpenRefine_ para definir el mapeo del esquema de los datos y la ontología creada en el apartado 2.4 y realizar la transformación en formato _RDF_:

<img width="404" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/33ede172-4ad9-4fbf-aafb-72615806419d">


<img width="406" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/d05b4614-5fec-4e19-8641-8214d9b3f71c">

- Resultado final tras la exportación del fichero _RDF/XML_. Se muestra una imagen del primer registro de datos. Se adjunta fichero en la carpeta _ExportRDF_:
  
  <img width="724" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/2eb89664-04f4-49e1-8712-99191fc9bf26">
  

### 2.6. Enlazado

Para darle un valor añadido a los datos y poder así enriquecer la información del dominio, se enlazan los datos csv con otros datos externos, obteniendo así, otras vías para explorar más información. Para ello, para realizar la reconcialiación, cotejo o enlace entre ambas fuentes de datos se utiliza la herramienta _OpenRefine_.

- Identificación de enlaces con otros conjuntos de datos en las columnas del dataset:
  - Como se trata de buscar información en otra fuente de datos, se descartan aquellas columnas que sean valores numéricos, valores como el tipo de edificio o su dirección. Por lo que, se buscan valores genéricos como nombres de ciudades, nombres de países. La columna que se ajusta a dichas carcterísticas para ser candidata en ser enlazada con otra fuente de datos es la columan que informa de la _Provincia_ de la certificación energética de los edificios.
 
- Enlace de datos:
  - Desde la aplicación _OpenRefine_ se realiza el cotejo de la columna _Provincia_ con [Wikidata](https://datos.gob.es/es/blog/wikidata-una-base-de-datos-de-conocimiento-libre-y-abierto#:~:text=%C2%BFQu%C3%A9%20es%20wikidata%3F,datos%20de%20otros%20repositorios%20digitales.), una base de datos de conocimiento libre y abierto:

    <img width="464" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/ac79beba-ee01-4674-a5d5-c473611e031e">
  - Tras realizar el cotejo, la columna queda enlazada con la información que proporciona _Wikidata_:

      <img width="151" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/c84852ee-affa-4087-bf84-437d0d2268c9">
      
- Información extra proporcionada desde el item [_chartered community (Q3297051)_](https://www.wikidata.org/wiki/Q3297051) de _Wikidata_:

   <img width="773" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/22d99137-b578-4f05-a926-6f83e9d0b63d">

- Nueva columna informando de la _URI_ a partir de la columna enlazada _Provincia_:
  - Se crea la columna _WikiDataProvincia_ a partir de la columna _Provincia_ informando de la URI:

    <img width="369" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/f683c3b1-636a-48c8-beb0-fb47cdd3431c">
    

    <img width="259" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/7bee3d69-2fa4-48a9-a03e-2f88cbed6037">

### 2.7. Publicación

Como los datos se actualizan diariamente, se procede con la publicación. El inconveniente es que en el proceso de publicación da el error: ... _request to https://api.datahub.io/auth/check? ](https://api.datahub.io/auth/check?jwt=&next=http://localhost:3000 failed, reason: certificate has expired_ y los datos no se han podido publicar desde [DataHub.io](https://datahub.io/). Se reportan todos lo pasos que se han seguido y se crea una [issue](https://github.com/AEPIA-WebSemanticaDatosEnlazados/Curso20222023/issues/16) en Github para compartir el problema.

Los pasos que se han llevado a cabo han sido los siguientes:

1. Acceso a [DataHub.io](https://datahub.io/) y de ahí a [OLD DataHub](https://old.datahub.io/) para crear una cuenta.
2. Creación de una cuenta con mi usuario y acceso al contenido:

   <img width="499" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/fd1f2938-7df3-4940-a213-d92dadf035f9">

3. Descarga e instalación de la herramienta [data](https://datahub.io/docs/features/data-cli),lectura de la [documentación](https://github.com/datopian/data-cli/blob/master/docs/push.md) y los [pasos](https://discuss.okfn.org/t/creating-a-dataset-on-the-datahub/1627) a seguir para la publicación de los datos:
   
   <img width="339" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/01cb1478-6a76-481a-84a4-570e0d860174">

5. Error al ejecutar el comando _data login_:

   <img width="666" alt="image" src="https://github.com/amvajua1/Curso20222023/assets/136450615/7fbb19bb-6174-432b-9d9b-5be6b60ca98d">

## 3. Aplicación y explotación (en construcción)






      

      



  




