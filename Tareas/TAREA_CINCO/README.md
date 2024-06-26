# TAREA 5: Uso de Pandas, Matplotlib y Numpy en Python


## Ejecución del programa:

Para ejecutar el programa, asegúrese de estar en el directorio del repositorio en su computadora y escriba el comando `make`, como se muestra a continuación:

```go
...\ie0217\Tareas\TAREA_CINCO> make
```

A partir del make se le mostrarán las gráficas y datos del CSV de la parte práctica 1 y el manejo de las calificaciones de la parte práctica 2.


## Parte práctica I:
> Para acceder al CSV utilizado en el análisis y codificación de la Parte Práctica I de la tarea, puedes visitar la siguiente página: [Air Carriers : T-100 International Market (All Carriers)](https://www.transtats.bts.gov/DL_SelectFields.aspx?gnoyr_VQ=FJD&QO_fu146_anzr=Nv4%20Pn44vr45). Es importante seleccionar la opción "Select all fields" en la página antes de proceder con la descarga para asegurarse de obtener la misma cantidad de información que se utilizó en el análisis.

### Estudio del CSV, limpieza y preparación de datos:
#### Información correspondiente a las columnas del CSV empleado:
| Categoría          | Columna                   | Descripción                                                                                            |
|--------------------|---------------------------|--------------------------------------------------------------------------------------------------------|
| ***Summaries***          | **Passengers**            | Mercado a bordo Pasajeros embarcados                                                                  |
|                    | **Freight**               | Mercado a bordo Carga embarcada (libras)                                                              |
|                    | **Mail**                  | Correo del mercado a bordo embarcado (libras)                                                         |
|                    | **Distance**              | Distancia entre aeropuertos (millas)                                                                  |
| ***Carrier***      | **UniqueCarrier**         | Código de Transportista Único. Este campo se utiliza para análisis a lo largo de varios años.          |
|                    | **AirlineID**             | Número de Identificación asignado por el Departamento de Transporte de EE. UU. para identificar una aerolínea única. |
|                    | **UniqueCarrierName**     | Nombre de Transportista Único                                                                         |
|                    | **UniqCarrierEntity**     | Entidad Única para la Región de Operación de un Transportista.                                         |
|                    | **CarrierRegion**         | Región de Operación del Transportista.                                                                |
|                    | **Carrier**               | Código asignado por IATA para identificar un transportista.                                            |
|                    | **CarrierName**           | Nombre del Transportista                                                                              |
|                    | **CarrierGroup**          | Código de Grupo de Transportista utilizado en análisis heredados.                                      |
|                    | **CarrierGroupNew**       | Nuevo Grupo de Transportista.                                                                |
| ***Origin***             | **OriginAirportID**       | ID del Aeropuerto de Origen                                                                           |
|                    | **OriginAirportSeqID**    | ID de Secuencia del Aeropuerto de Origen                                                              |
|                    | **OriginCityMarketID**    | ID del Mercado de la Ciudad de Origen del Aeropuerto                                                  |
|                    | **Origin**                | Aeropuerto de Origen                                                                                  |
|                    | **OriginCityName**        | Nombre de la Ciudad del Aeropuerto de Origen                                                          |
|                    | **OriginCountry**         | País de Origen del Aeropuerto                                                                         |
|                    | **OriginCountryName**     | Nombre del País de Origen del Aeropuerto                                                              |
|                    | **OriginWac**             | Código de Área Mundial del Aeropuerto de Origen                                                       |
| ***Destination***            | **DestAirportID**         | ID del Aeropuerto de Destino                                                                          |
|                    | **DestAirportSeqID**      | ID de Secuencia del Aeropuerto de Destino                                                             |
|                    | **DestCityMarketID**      | ID del Mercado de la Ciudad de Destino del Aeropuerto                                                 |
|                    | **Dest**                  | Aeropuerto de Destino                                                                                 |
|                    | **DestCityName**          | Nombre de la Ciudad del Aeropuerto de Destino                                                         |
|                    | **DestCountry**           | País de Destino del Aeropuerto                                                                        |
|                    | **DestCountryName**       | Nombre del País de Destino del Aeropuerto                                                             |
|                    | **DestWac**               | Código de Área Mundial del Aeropuerto de Destino                                                      |
| ***Time Period***  | **Year**                  | Año                                                                                                    |
|                    | **Quarter**               | Trimestre                                                                                               |
|                    | **Month**                 | Mes                                                                                                    |
| ***Other***              | **DistanceGroup**         | Intervalos de Distancia, cada 500 Millas, para Segmentos de Vuelo                                      |
|                    | **Class**                 | Clase de Servicio                                                                                      |


##### Las clases de servicio existentes: 
- **A**: "Servicio de Pasajeros de Primera Clase Programado/ Servicio de Carga A"
- **C**: "Servicio de Pasajeros de Clase Económica Programado/ Servicio de Carga C"
- **E**: "Servicio Programado de Pasajeros y Carga Mixta, de Primera Clase y Clase Económica E"
- **F**: "Servicio Programado de Pasajeros y Carga F"
- **G**: "Servicio Programado de Carga Únicamente G"
- **H**: "Razón Humanitaria No Programada, No Generadora de Ingresos"
- **K**: "Servicio Programado K (F+G)"
- **L**: "Servicio No Programado Civil de Pasajeros y Carga L"
- **N**: "Servicio No Programado Militar de Pasajeros y Carga N"
- **P**: "Servicio No Programado Civil de Carga Únicamente P"
- **Q**: "Servicios No Programados (Excepto Chárter) Q"
- **R**: "Servicio No Programado Militar de Carga Únicamente R"
- **V**: "Servicio No Programado V (L+N+P+R) para Transportista de EE. UU. y (L+P+Q) para Transportista Extranjero"
- **Z**: "Todo Servicio Z (K+V)"

#### Limpieza y preparación de Datos:
Como se puede observar en la sección anterior, el CSV tiene muchas columnas, sin embargo, algunas de ellas no resultan relevantes para el propósito de este trabajo. Por ejemplo, la columna `Carrier`, que contiene el código IATA que identifica a las aerolíneas, no aporta información significativa, ya que este análisis se centra en aspectos como pasajeros, vuelos y tiempos de vuelo, en lugar de datos institucionales específicos. De la misma forma hay varias columnas cuyo aporte es nulo, a continuación se va a mostrar una tabla con las columans eliminadas y su justificación:

| Columna              | Motivo de eliminación                                                                                                                      |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Mail                 | La mayoría de los datos en esta columna son ceros y no aportan información relevante sobre el peso del correo enviado en libras.           |
| UniqueCarrier        | No es necesario conocer el código único del transportista; generalmente, los pasajeros prestan más atención al nombre de las aerolíneas.  |
| AirlineID            | El identificador asignado por el Departamento de Transporte de EE.UU. para cada aerolínea no aporta información útil en este análisis.   |
| UniqCarrierEntity    | La entidad única de operación de los transportistas se presenta con un ID que no ofrece información clara sobre la región de operación. |
| CarrierRegion        | Los acrónimos en esta columna no especifican claramente la región de operación y pueden resultar confusos sin un contexto adicional.    |
| Carrier              | El código asignado por IATA para identificar a los transportistas no es necesario para este análisis.                                    |
| CarrierName          | Aunque el nombre del transportista es importante, esta información se comparte con la columna UniqueCarrierName.                        |
| CarrierGroup         | El número que especifica el grupo de transportista puede prescindirse ya que otras columnas indican el país de origen y destino.         |
| CarrierGroupNew      | Este campo representa lo mismo que CarrierGroup pero con identificadores más específicos, que tampoco son necesarios para este análisis. |
| OriginAirportID      | El ID del aeropuerto no es necesario cuando se tiene el nombre del aeropuerto como identificador.                                       |
| OriginAirportSeqID   | Similar a OriginAirportID, este identificador no es relevante para el análisis y puede omitirse.                                        |
| OriginCityMarketID   | El identificador del mercado de la ciudad de origen del aeropuerto no aporta información significativa para este análisis.               |
| Origin               | La representación del aeropuerto de origen en forma de acrónimos no es necesaria cuando se tiene la ciudad de origen del aeropuerto.     |
| OriginCountry        | Los acrónimos de los países de origen pueden ser omitidos ya que hay una columna que proporciona el nombre completo del país.             |
| OriginWac            | El código de área mundial del aeropuerto de origen puede omitirse ya que se puede obtener el país de origen del aeropuerto.             |
| DestAirportID        | Al igual que con OriginAirportID, el ID del aeropuerto de destino no es necesario cuando se tiene el nombre del aeropuerto.             |
| DestAirportSeqID     | Similar a DestAirportID, este identificador no es relevante para el análisis y puede ser omitido.                                        |
| DestCityMarketID     | El identificador del mercado de la ciudad de destino del aeropuerto no aporta información significativa para este análisis.               |
| Dest                 | La representación del aeropuerto de destino en forma de acrónimos no es necesaria cuando se tiene la ciudad de destino del aeropuerto. |
| DestCountry          | Los acrónimos de los países de destino pueden ser omitidos ya que hay una columna que proporciona el nombre completo del país.           |
| DestWac              | El código de área mundial del aeropuerto de destino puede omitirse ya que se puede obtener el país de destino del aeropuerto.           |
| Quarter              | La información del trimestre no es necesaria cuando se tienen las columnas de año y mes.                                                  |
| DistanceGroup        | No es necesario conocer los identificadores de grupos que representan la distancia en millas entre los aeropuertos, ya que esta información ya está disponible en otra columna. |

De esta forma se pasa de tener un DataFrame de 34 columnas a 11 columnas con datos verdaderamente relevantes para el análisis. Luego se estudia si dentro de las columnas restantes hay valores nulos, pero no se encontró ninguno, para ello hay un código que hace la verificación.

### Comparación de cantidad de pajeros por clase de la aerolinea:
La imagen titulada ***Distribución de pasajeros por clase***. Compara el número de pasajeros en diferentes clases, en este caso se puede observar que las unicas clases presentes en la gráfica son F, G, L y P. El análisis revela lo siguiente:: 

- **Clase F**: Esta clase tiene un número significativamente mayor de pasajeros (194512934.0) en comparación con las demás, y esto representa el Servicio Programado de Pasajeros y Carga. Considerando que la mayoria de pasajeros en viajes largos llevan maletas tiene mucho sentido que la denominación F sea la más usada de las clases.

- **Clase G**: Esta clase no tiene pasajeros, porque esta solo brinda servicios de carga.
- **Clase L**: Esta clase tiene un número moderado de pasajeros (1161470.0), esto se debe a que se trata de servicios no programados para pasajeros. Los servicios no programados se todos aquellos vuelos que por algun imprevisto, como problemas climáticos, tuvieron que salir sin un horario programado.
- **Clase P**: Esta clase tiene un número muy pequeño de pasajeros (107.0), pero esto se debe a que son servicios de carga no programados. A pesar de que dicte que solo son servicios de carga hay un recuento de pasajeros por lo que se podría considerar el hecho que sean trabajadores de la misma aerolinea que no son pilotos.

La clase que más destaca es la comparación de la clase F y Clase G, debido a que ambas representan lo mismo pero lo que cambia es si los viajes son programados o no. Comparando la cantidad de pasajeros, se puede considerar que la mayoría de aerolineas no presentan retrazos o problemas climáticos que haga que sea necesario crear vuelos no programados, y esto se debe un retraso de este serviso de transporta es el que genera más perdidas de todos los posibles por lo que considerar un vuelo no programado podría constar de muchas perdidas monetareas.

<img src="../TAREA_CINCO/Material_Practica/Pasajeros_x_clase.svg">

### Comparación de cantidad de peso por clase de la aerolinea:
La imagen titulada ***Distribución de peso por clase***. Compara el la cantidad porcentual de peso en diferentes clases, en este caso se puede observar que las unicas clases presentes en la gráfica son F, G, L y P. El hecho que se repitan las clases en este gráfico tiene como motivo que son las únicas clases observadas por el CSV seleccionado.

El análisis revela lo siguiente:

- **Clase F**: Transportó un total de 5,498,593,187.0 libras.
- **Clase G**: Registró un peso de 8,363,143,404.0 libras.
- **Clase L**: Transportó 19,946,616.0 libras.
- **Clase P**: Registró un peso de 4,128,241,176.0 libras.

Se observa que todas las clases transportaron una cantidad porcentual de peso significativa, reflejando la diversidad de cargas manejadas por cada una. La clase F, siendo la segunda porción más grande, se explica debido a su enfoque en el transporte de pasajeros que llevan equipaje (cada uno con su peso respectivo). Por otro lado, la clase L, que representa los vuelos no programados, exhibe la menor cantidad de peso, ya que estos son menos frecuentes.

Por otro lado, la clase G destaca por su elevado peso (la porción más grande), lo cual se atribuye a su servicio exclusivo de carga que se brinda. Similarmente, la clase P representa el peso en vuelos no programados, lo cual contribuye a su carga significativa.
<img src="../TAREA_CINCO/Material_Practica/Peso_x_clase.svg">

### Comparación de cantidad de pasajeros por aerolinea:
> Se seleccionaron las primeras 10 aerolíneas y las últimas 10 aerolíneas del archivo CSV. Esta selección no siguió ningún criterio técnico específico, sino que se realizó con el fin de garantizar que el gráfico resultante fuera fácilmente observable y comprensible. Dada la gran cantidad de más de 300 aerolíneas presentes en el archivo CSV, utilizarlas todas no sería práctico y el análisis resultaría demasiado extenso.

El análisis se enfoca en las aerolíneas con mayor y menor número de pasajeros durante el año 2023, a partir de la gráfica de puntos ***Distribución de pasajeros por aerolinea***, buscando entender por qué la gran diferencia en cantidad se realizó hacer una busqueda en páginas de web de forma superficial y justificar los datos.

Entre las aerolíneas con más pasajeros se encuentran:

- **Westjet:** Líder con casi 4 millones de pasajeros en 2023, destaca por su amplia red de más de 100 destinos en América, Europa y Asia, así como por su reputación de ofrecer tarifas competitivas y servicio al cliente de calidad.
  
- **Vistajet Limited:** Segunda en la lista con más de 2 millones de pasajeros en 2023, se especializa en vuelos chárter de lujo para clientes de alto perfil, respaldado por una flota extensa y una presencia global en más de 180 países.

- **Vuela EL Salvador S.A. de C.V.:** Ocupando el tercer lugar con más de 167 mil pasajeros, se destaca como una subsidiaria de Volaris, centrada en vuelos de bajo costo desde y hacia El Salvador, conectando con diversos destinos en América del Norte y Centroamérica.

- **Western Air Charter, Inc. d/b/a Jet Edge:** Con más de 306 mil pasajeros, esta aerolínea de aviación privada se especializa en vuelos corporativos y de lujo, con una amplia flota y presencia en más de 50 países.

- **Xiamen Airlines Co., Ltd:** A pesar de registrar más de 59 mil pasajeros, es una de las aerolíneas más grandes de China, con una extensa red que abarca Asia, Europa, América y Oceanía, siendo parte de la alianza SkyTeam.

Las aerolíneas con menos pasajeros presentan un conjunto diferente de características:

- **ABSA-Aerolinhas Brasileiras, ABX Air Inc., ACM AIR CHARTER GmbH y Western Global:** Empresas de carga aérea sin servicios de pasajeros, lo que explica su ausencia de pasajeros registrados.

- **ABS JETS A.S., AVCON JET MALTA LTD, AXIS Aviation Switzerland AG y Acropolis Aviation Ltd.:** Operan en el segmento de aviación privada, pero con flotas más pequeñas y operaciones limitadas principalmente a Europa, sirviendo a una clientela muy selecta.

- **ADVANCED AIR, LLC, Aer Lingus Plc y Vuela Aviation, S.A.:** Aunque son aerolíneas de pasajeros, tienen una oferta limitada en términos de destinos y frecuencias, lo que reduce su atractivo para los viajeros.

<img src="../TAREA_CINCO/Material_Practica/Pasajeros_x_aerolinea.svg">

### Comparación de las 5 aerolineas con mayor distancia reccorida y las 5 aerolineas con menor distancia, dentro del CSV:

El análisis se centra en la imágem de esta sección, la cual trata de la distancia recorrida por cada aerolínea, destacando aquellas con los trayectos más largos y más cortos durante el año 2023, además de el país de salida de cada aerolinea. Haciendo un poco de investigación en las primeras páginas que hablan sobre cada aerolinea se pudo determinar los motivos de por qué tuvieron esos resultados en el recorrido, ya que usualmente se asocia una mayor distancia a mayor tiempo de trabajo, aunque eso no representa que haya mayor o menor ganancia.

El análisis se enfoca en la distancia recorrida por cada aerolínea, destacando aquellas con los trayectos más largos y más cortos durante el año 2023.

Entre las aerolíneas con mayor recorrido se encuentran:

1. **United Airlines Inc - United States:** Conocida como la mayor aerolínea del mundo en términos de pasajeros transportados y alcance global. Operando vuelos a más de 300 destinos en 60 países, su distancia recorrida es la más alta del gráfico, reflejando su amplia presencia y demanda global.

2. **Delta Air Lines Inc. - México:** Como subsidiaria de Delta Air Lines, una de las principales aerolíneas de Estados Unidos, Delta Air Lines Inc. registra una distancia recorrida significativa, indicando una buena presencia en el mercado mexicano y regional, y sus vuelos interacionales.

3. **American Airlines Inc - United States:** Como una de las aerolíneas más grandes y antiguas de Estados Unidos, American Airlines Inc. compite por el liderazgo en el mercado estadounidense e internacional con una distancia recorrida similar a Delta Air Lines.

4. **Vistajet Limited - Canada:** Aunque de bajo costo, Vistajet Limited muestra una distancia recorrida moderada. Esto se puede deber que al ser su costo menor su oferta limitada de rutas y destinos en comparación con las principales aerolíneas, demostrando así que no se puede asociar distancias con una ganancia especifica para una aerolinea si es que no se cuentan todos los casos.

5. **Korean Air Lines Co., Ltd - Dominican Republic:** Aunque es una de las aerolíneas más grandes de Asia, su distancia recorrida es la más baja del gráfico, esto se puede deber a que Republica Dominicana no genera muchas rutas de salida a otros paises y los viajes regionales serían poco comunes a comparación de Estados Unidos debido a una mucha menor extensión de territorio.

Por otro lado, las aerolíneas con menor recorrido fueron:

1. **Flighcreaft Air Charter aba KF Aeroflyer - The Bahamas:** Aunque ofrece servicios de transporte de pasajeros y carga entre las Bahamas y el Caribe, su distancia recorrida es baja, lo que sugiere un enfoque en vuelos regionales y locales, o que durante el 2023 la presencia de turismo a disminuido debido a la inflación y la todavía recuperación del Covid-19.

2. **Western Air Ltd - United States:** Aunque ofrece vuelos diarios entre las principales rutas se encuentra las Bahamas y el Caribe, su distancia recorrida es baja, indicando así que el turismo de por parte de los americanos no esta especialmente enfocado en esos paises. Esto del turismo se podría deber un poco a las corrientes ideológicas que chocan fuertemente entre el Capitalismo de Estados Unidos y la presencia de Socialismo en los países del Caribe.

3. **Talofa Airways Limited - United Stades:** Especializada en vuelos dentro de la región polinesia, y considerando que la isla de Hawai se encuentra en esa región y los viajes en si son cortos, podría tratase de una aerolinea de viajes de entrada y salida la isla hawaiana.

4. **Golden Wings Charter Ltd - Canada:** Especializada en transporte aéreo ejecutivo unicamente, su distancia recorrida es baja, sugiriendo vuelos personalizados y flexibles según las necesidades de los clientes, aunque muy caros. Debido a la exclusividad no se puede decir que sus recorridos serán largos y repetidos.

5. **HARBOUR AIR LTD DBA HARBOUR AIR SEAPLANES WHISTLER AIR AND SALTSPRING AIR - United Stades:** Como la mayor aerolínea de hidroaviones de América del Norte, su distancia recorrida es baja, dedicándose a vuelos locales y escénicos cerca de la costa oeste de Canadá.

<img src="../TAREA_CINCO/Material_Practica/Aerolineas_x_distancia.svg">

## Parte teórica:
### Iteradores
1. ¿Qué es un iterador en Python y cuál es su propósito?
Los iteradores son métodos que iteran (se mueven a travez de la información) listas, tuplas, ordered sets, diccionarios y cualquiera otro tipo dato que almacene información en su interior separada por indices. Se utiliza para recorrer un coleccionable (objeto) y devolver sus elementos.

Un objeto iterador en Oython debe usar métodos mágicos como `__iter__()` y `__next()__`, denominados protocolos iterador, para recorrer un coleccionable. 

2. Explica la diferencia entre un iterable y un iterador.

Un **iterable** es un objeto que se puede recorrer con un bucle `for`, como una lista, una tupla o una cadena de texto. 

Un iterable hace uso de los protocolos iterador: `__iter__()` que devuelve un **iterador** y `__next__()` que devuelve el siguiente elemento del iterable. Un iterador se agota cuando no hay más elementos que devolver y lanza una excepción `StopIteration`.

Por ejemplo, si se tiene un coleccionable tupla, este es un iterable, y cuando se usa el método `iter(tupla)` pasa a ser un iterador y al usar el método `next()` se obtienen elementos del iterador uno a uno, hasta que se agote.

```python
# Se crea una tupla
tupla = (1, 2, 3, 4, 5)

# Se saca un iterador de la tupla
iterador = iter(tupla)

# Método next() para obtener los elementos del iterador
print(next(iterador))   # Output: 1
print(next(iterador))   # Output: 2
print(next(iterador))   # Output: 3
print(next(iterador))   # Output: 4
print(next(iterador))   # Output: 5
print(next(iterador))   # Output: Error StopIteration
```

### Excepciones
1. Define qué es una excepción en Python.

Una excepción es un objeto (como todo en Python) que representa una condición inusual que ocurre durante la ejecución de un programa, principalmente ocurre cuando se sale del *HappyPath*. Este objeto puede ser lanzado o lanzados cuando ocurre un error o una condición especial, y pueden ser capturados y manejados para evitar que el programa se detenga abruptamente. 

2. ¿Cuál es el propósito de la cláusula try...except en el manejo de excepciones?

El propósito del try/except es gestionar los errores y excepciones que puedan ocurrir durante la ejecución de un programa, impidiendo que el programa se pare o haciendo que el usuario solo ingrese lo esperado. 

Para hacer uso de esta cláusula, en el bloque `try` se coloca el código que se va a ejecutar y en uno o varios bloques `except` se coloca lo que se va a desplegar si ocurre un comportamiento no deseado.

Un ejemplo de uso puede ser cuando hay una división y el denominador es 0:

```python
try:
  resultado = num1 / num2
  print(f"El resultado de la división es {resultado}")
except ZeroDivisionError:
  # Si num2 es 0, se despliega la siguiente excepción
  print("Error: No se puede dividir por cero")
```

3. Explica la diferencia entre las cláusulas except y finally en el manejo de excepciones.

El `except` se ejecuta cuando el bloque try lanza una excepción de un tipo específico que se indica en la cláusula. Esta cláusula permite capturar y manejar el error, evitando que el programa se detenga o se comporte de forma inesperada. Se puede tener más de una cláusula except para diferentes tipos de excepciones.

El `finally` se ejecuta siempre, independientemente de si el bloque try lanza una excepción o no, o si se captura o no. Esta cláusula permite liberar recursos, como cerrar un file previamente abierto, o realizar acciones de limpieza que se deben hacer siempre al finalizar la ejecución de un bloque de código.

Reutizando el ejemplo anterior:

```python
try:
    resultado = num1 / num2
    print(f"El resultado de la división es {resultado}")
except ZeroDivisionError:
    # Si num2 es 0, se despliega la siguiente excepción
    print("Error: No se puede dividir por cero")
finally:
    # Esto siempre se ejecutará, con o sin presencia de excepción
    print("Se término la división de num1 y num2")
```
### Generadores
1. ¿Qué es un generador en Python y cuál es su ventaja sobre las listas tradicionales?

Un generador es una función que devuelve un iterador que puede producir una secuencia de valores de unicamente cuando se le solicita, sin generarlos todos de una vez. Su principal ventaje sobre las listas tradicionales es que son más eficientes en el uso de la memoria, ya que solo almacenan el estado de la función y no toda la secuencia de valores [1]. Además, los generadores pueden operar sobre muy grandes o casi infinitos, que no cabrían en una lista por el espacio de memoria que requieren [1].

2. Explica cómo se puede crear un generador usando la función yield.

Se puede definir una función generadora usando la palabra calve `yield` dentro de la definición de la función en lugar del `return`. La función yield devuelve un valor y pausa la ejecución de la función, conservando su estado para reanudarla cuando se le vuelva a llamar. 

Por ejemplo, el siguiente código define un generador que produce los números pares:

```python
def generador_pares(loop):
    n = 0
    while n < loop*2:
        yield n
        n += 2


# Se coloca la cantidad de número pares que se desean obtener
pares_generados = generador_pares(3)

# Iterar sobre los valores generados e imprimirlos
for valor in pares_generados:
    print(valor)        # Output: 0 > 2 > 4
```

3. ¿Cuándo es más apropiado usar generadores en lugar de listas?

Es más apropiado usar generadores en lugar de listas cuando se quiere procesar una secuencia de datos de forma en varias ocasiones dentro del código, sin necesidad de almacenarla toda en memoria, o cuando se quiere trabajar con datos infinitos o muy grandes, que no se podrían generar o almacenar en una lista [1].


### Pandas
1. ¿Cuál es la diferencia entre una Serie y un DataFrame en Pandas?

Una Serie es un objeto de una sola dimensión que puede contener cualquier tipo de datos, como enteros, flotantes, cadenas, etc; como lo sería una lista. Estos tienen un índice que identifica cada elemento de la Serie y se puede considerar como una columna de un conjunto de datos. 

Un DataFrame es un objeto dos dimensiones que puede contener varias Series, cada una con su propio nombre y tipo de datos. Tiene un índice de filas y un índice de columnas que identifican cada fila y cada columna del DataFrame y se puede considerar como una tabla de datos de un excel. 

Otra diferencia es como se crea una Serie y Un DataFrame en Pandas:

```python
# Se importa la librería de pandas
import pandas as pd

# Serie con números enteros y un índice alfabético
s = pd.Series([10, 20, 30, 40], index=["a", "b", "c", "d"])

# DataFrame con dos Series, una de números enteros y otra de cadenas, y un índice numérico
df = pd.DataFrame({"numeros": [1, 2, 3, 4], "nombres": ["Ana", "Beto", "Carlos", "Diana"]}, index=[1, 2, 3, 4])
```

2. Explica cómo manejar valores nulos o faltantes en un DataFrame.

Los valores nulos o faltantes en un DataFrame se representan con el valor especial NaN, y la libería de pandas ofrece varios métodos para manejar estos valores [2]. Algunas de las opciones más comunes investigadas son las siguientes:

- Eliminar las filas o columnas que contengan valores nulos con el método `dropna()`. Se puede especificar el eje (0 para filas, 1 para columnas), el umbral (número mínimo de valores no nulos para conservar la fila o columna) y el subconjunto (lista de columnas a considerar para la eliminación) [3].

- Rellenar los valores nulos con un valor constante con el método `fillna()`. Se puede especificar el valor a usar, el eje, el método (para usar el valor anterior o posterior al nulo) y el límite (número máximo de valores nulos a rellenar) [3].

- Reemplazar los valores nulos con un valor calculado con el el método `replace()`. Se puede especificar el valor a reemplazar, el valor a usar (casi siempre 0), el método y el límite. También se puede usar una función o un diccionario para definir el valor a usar según el valor a reemplazar [2].

- Interpolar los valores nulos con un valor estimado con el el método `interpolate()`. Se puede especificar el método de interpolación (lineal, cuadrático, cúbico, etc.), el eje, el límite y el orden (para los métodos polinomiales) [2].

3. ¿Cuál es la diferencia entre loc y iloc en Pandas?

Ambos métodos el`loc` e `iloc` tiene la función de seleccionar filas y columnas de un DataFrame. La diferencia entre ellos es que `loc` se basa en las etiquetas de los índices, mientras que `iloc` se basa en las posiciones de los índices [4].

## Bibliografía:

[1] “Generators - Learn Python - Free Interactive Python Tutorial,” Learn Python, [Online]. Disponible: https://www.learnpython.org/es/Generators. [Accedido: 04- Feb- 2024].

[2] "N. Urrego, 'Tratamiento de valores vacíos I: Cómo abordar datos incompletos en tu dataset,' Medium, 25-Jul-2023. [Online]. Disponible: https://medium.com/@nicolasurrego/tratamiento-de-valores-faltantes-i-c%C3%B3mo-abordar-datos-incompletos-en-tu-dataset-35d51c522842. [Accedido: 04- Feb- 2024]."

[3] S. Kundu, “The Pandas fillna and dropna Methods”, Medium, 2020. [Online]. Disponible: https://medium.com/@sagnikkundu25/the-pandas-fillna-and-dropna-methods-1fecad724aa9#:~:text=In%20many%20cases%2C%20you%20will%20want%20to%20replace,value.%20This%20is%20what%20the%20dropna%20method%20does.. [Accessed: 04- Feb- 2024].

[4] “Difference between loc() and iloc() in Pandas DataFrame,” GeeksforGeeks, [Online]. Disponible: https://www.geeksforgeeks.org/difference-between-loc-and-iloc-in-pandas-dataframe/. [Accedido: 04- Feb- 2024].