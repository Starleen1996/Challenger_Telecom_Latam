#### INTRODUCCIÓN DEL PROYECTO:
Actualmente la compañia TelecomX_Latam ofrece diferentes servicios de telecomunicación; como servicio a internet, peliculas, ofrece servicios de protección y respaldo. En este orden de ideas, queremos mostrarle a la compañia como ha sido el comportamiento de sus clientes, es decir, vamos a establecer metricas sobre la evasión (retiro y permanencia) de estos, para establecer conclusiones que nos ayuden a proponer estrategias para aumentar la afiliación  de nuevos cliente y fidelizarlos. 
Adicionalmente, queremos visualizar como ha sido el comportamiento de la compañia en diferentes aspectos como: tipo de cliente, tipo de servicios, gastos totales, tipos de contratos, tiempo de contratos para analizar con mayor facilidad el rumbo y estado actual de la misma y tratar de entender la evasión de clientes.

**Limpieza y Tratamiento de Datos: Describe los pasos realizados para importar, limpiar y procesar los datos**

Para dar inicio con el análisis de datos y construir la información, hemos obtenido la base de datos con la compañia **TelecomX_Latam**.

Dirección Base de Datos: https://raw.githubusercontent.com/Starleen1996/Challenger_Telecom_Latam/refs/heads/main/TelecomX_Data.json"

Esta base de datos se encuentra en un archivo con extensión JSON, donde requeriamos hacer la importación de los datos a **google colab**

Pasos realizados para la importación

1. Uso de la biblioteca JSON:
- import requests
- import json

Con estas bibliotecas podiamos importar la base de datos, la cual se encontraba en un github.

A continuación mostramos el código utilizado para leer el archivo JSON en google Colab y posteriormente convertirlo en un Dataframe llamado **"df_clientes_LATAM"**

- df_clientes_LATAM = pd.read_json(url)
- df_clientes_LATAM

-- Pasos realizados para la organización del Dataframe **"df_clientes_LATAM"**

una vez realizamos la visualización del dataframe **"df_clientes_LATAM"**, identificamos que algunas columnas se encontraban anidadas, es decir, columnas con diccionarios, lo cual, no permitia tener una visualización a detalle de los datos.Por ende, requeriamos ordenar nuevamente este dataframe.

Para ello, aplicamos el metodo normalize al Dataframe **"df_clientes_LATAM"**, para desanidar las columnas que contenian diccionarios. Tal cual como se muestra a continuación:

- df_clientes_LATAM = pd.json_normalize(df_clientes_LATAM)
- df_clientes_LATAM

Finalmente obtenemos un dataframe con 7267 filas y 21 columnas.

-- Posteriormente visualizamos los diferentes datos que estan contenidas en cada una de las columnas del dataframe, para ello utilizamos el metodo **"unique"** el cual nos permite ver los datos unicos en cada una de las columnas

-- Posteriormente verificamos si tenemos datos duplicados y nulos en cada una de nuestras columnas, para ello utilizamos los metodos "duplicated" y "isnull" posteriormente realizamos la suma de estos, para saber cuales datos debemos limpiar y transformar.

--Posteriormente aplicamos la función applymap y replace con el metodo strip() para elimitar datos con espacios o vacios y limpiar nuestro data frame.

-- Posteriormente llamamos llamamos nuestro datframe df_clientes_LATAM.info(), con este podemos visualizar el tipo de columna que contiene el dataframe y poder realizar cambios en el tipo de datos para futuros análisis.

**Manejo de Inconsitencias**

Para el manejo de inconsistencias en nuestro Dataframe **df_clientes_LATAM** establecemos lo siguiente:

1. definimos el nombre de las columnas en letra minuscula para facilitar la lectura de cada columna. Tambien cambiamos el nombre de las columnas, ya que estas estaban en inglés y esto nos facilita entender mejor los datos por columna.
2. las columnas que estan compuestas por 2 palabras o mas, se asigna el "_" para evitar el uso de espacios.
3. Las columnas que contenian datos como "YES/NO" fueron cambiadas por "1/0" para establecer los números binarios y facilitar la cuantificación de los datos.
4. En algunas columnas habian datos con "No internet service", estos se cambiaron por el número "0", ya que ciertos clientes no tenian  servicio de internet y evitar errores en la cuantificiación de los datos.
5. Limpiamos algunos datos en la columna "account_charges_total" y convertir la columna "account_charges_total" a **float64**, para esto hicimos la importación de la biblioteca **Numpy** para hacer el cambio de tipo de dato.
6. Realizamos la creación de una nueva columna llamada **"Cuentas_Diarias"**, la cual un requerimiento del cliente
7. Finalmente realizamos una revisión estadistica del dataframe con el metodo **describe()** con este, podemos ver información como la media,mediana, desviación std,quartiles, entre otros datos que nos puedan ayudar analizar la info del dataframe.

## Análisis Exploratorio de los Datos

Para iniciar con el análisis de los datos definidos en nuestro Dataframe **df_Clientes_LATAM** realizamos el uso de las siguientes bibliotecas:

* import matplotlib.pyplot as plt
* import seaborn as sns
* import plotly.express as px

estas últimas nos permitieron realizar un análisis estadistico construyendo diferentes visualizaciónes y/o graficos como: Histogramas, Diagrama de caja, Diagrama de torta/circulas, Diagrama de barras entre otros.

Cada una de estas bibliotecas presentan diferentes caracteristicas las cuales nos permiten establecer graficos e insight indicados para entender con mayor facilidad la información que queremos mostrar.

**Nota:** Tuve dificultad en el momento de seleccionar el tipo de grafico en relación a las columnas que queria comparar, ya que no habia una correlación entre ellas.

**Lista de graficos definidos para el análisis de la información de la empresa TelecomX_LATAM:**

1. Proporcion de Clientes Vigentes vs No Vigentes: Para la construcción del diagrama se uso la biblioteca Matpltlib y el grafico "plt.pie" el cual nos definió un grafico de torta. En esta visualización identificamos la proporción de los clientes vigentes y No vigentes de la compañia.
2. Clientes por Genero vs Estado de Vigencia: Para la construcción del diagrama se utilizo la biblioteca SeaBorn, la cual tiene mas opciones en colores y estetica del grafico "plt.bar". En este grafico visualizamos la cantidad de clientes por genero (hombre y mujer) en relación a la evasión (vigentes/No Vigentes).
3. Tipo de contrato vs Clientes Vigentes/ No Vigentes: Al igual se define un grafico de barras con el uso de la bibliteca SeaBorn, para visualizar el tipo de contrato vs Clientes Vigentes/No Vigentes.
4. Visualización de Clientes con edad >= 65 años y menor a 65 años vs Vigentes/No Vigentes: Se realiza la construcción de 2 diagramas para visualizar la cantidad de clientes en determinada edad y su evasión (vigente/No vigente) en la compañia.
5.Visualización de datos : Clientes Vigentes/ No Vigentes vs Metodo de Pago: Logramos visualizar la evasión de clientes (vigentes/No Vigentes) en relación al "metodo de pago" utilizado.
6. Distribución del Total Gastado por Estado de Vigencia: Utilizamos un grafico tipo Histograma de la biblioteca SeaBorn, para visualizar la distribuación de los datos. En este se comparan la "cantidad de clientes" sobre el "total gastado en el mes".
7.Distribución del Tiempo de Contrato por Estado de Vigencia: En este se compara la distribución de los datos en las variables "Tiempo del contrato vs Estado de vigencia(Evasión).
8. Diagrama de caja (boxplot): Este diagrama nos permite identificar la disperción de los datos a traves de los cuartiles, la mediana, el limite inferior y superior. Para ello se definieron 2 graficas:
* Total Gastado por Estado de Vigencia
* Tiempo de Contrato por Estado de Vigencia

##  Conclusiones e Insights: 
Resume los principales hallazgos y cómo estos datos pueden ayudar a reducir la evasión.

**Grafico Proporcion de Clientes Vigentes vs No Vigentes**
1. Evidenciamos que el 73.5% de los clientes se han retidado de la compañia , es decir no estan vigentes actualmente. Esto representa una alta evasión para la compañia.
**Grafico Clientes por Genero vs Estado de Vigencia**
2. Verificando a traves del grafico de barras la cantidad de clientes por genero (hombres y mujeres) pudimos identificar que su relación frente a la evasión, tiene un comportamiento similar. Como lo mensionamos en el grafico de proporción, la evasión es superior respecto a los clientes que continuan en la compañia, esto último, No difiere a que la tendencia de la evasión corresponda al tipo de genero.
**Grafico tipo de contrato vs Clientes Vigentes/ No Vigentes**
3. Podemos evidenciar en la visualización de las columnas: **Tipo de contrato** y *clientes que estan "Vigentes" y "No Vigentes"**, que los clientes con contratos a **1 año y 2 años** , han representado la mayor tasa de retiro (evasión) de la compañia.
Diferente para los clientes que tienen contrato **mes a mes**, aunque la tasa de evasión es superior a la tasa de permanencia, estos han mantenido un mayor tiempo en la compañia, manteniendo una relación mas proporcional (2220 clientes No Vigentes, 1655 Clientes Vigentes).
**Visualización de Clientes con edad >= 65 años y menor a 65 años vs Vigentes/No Vigentes**
4. Evidenciamos una superioridad en la cantidad de clientes menor a 65 años, en la cual se evidencia una tendencia en el retiro de personas de la compañia (evasión) . Clientes No Vigentes <65 : 4508 y clientes Vigentes <65 años: 1393 clientes. Finalmente podemos inferir que los clientes mas jovenes, tienen a realizar mas cambios en la empresa de servicios de telecomunicaciones.

**Visualización de datos : Clientes Vigentes/ No Vigentes vs Metodo de Pago**
5. Podemos observar que los clientes que representan mayor vigencia en la compañia son los que usan la forma de pago: Electronic Check.

**Conteo de evasión por variables numéricas**
6. Distribución del Tiempo de Contrato por Estado de Vigencia (Histograma)
- Conclusiones generales:
- 📉 Alta tasa de cancelación temprana: Muchos clientes se retiran en los primeros meses de contrato.
- 💰 Bajo gasto = alta rotación: Clientes que gastan poco tienden a no seguir.
- ⏳ Tiempo y gasto = vigencia: Clientes con más tiempo y gasto son más propensos a permanecer.

**Boxplot: Total Gastado por Estado de Vigencia**
- Interpretación estadística:

Clientes No Vigentes (0, en rojo):
Tienen una mediana de gasto más alta.
Presentan una mayor dispersión (más amplitud entre mínimo y máximo).
Hay muchos valores altos (gastos elevados), pero también valores bajos.

Clientes Vigentes (1, en gris):
La mediana es notablemente más baja.
A pesar de haber outliers con gasto alto, la mayoría se concentra en rangos bajos (entre 0 y ~2.000).
Esto refuerza la idea de que estos clientes están en una etapa temprana de su ciclo de compra.

**Conclusión del informe**
El gasto total acumulado es mayor en clientes no vigentes. 
Esto puede explicarse por el hecho de que han tenido relaciones contractuales más largas, permitiéndoles realizar más compras. 
Por su parte, los clientes vigentes muestran gastos significativamente más bajos, posiblemente asociados a contratos recientes o menor frecuencia de consumo.

**Boxplot: Tiempo contrato vs estado de vigencia**

Clientes No Vigentes (0, en rojo):
Tienen una mediana del tiempo de contrato más alta (alrededor de 38 meses).
El rango intercuartílico (IQR, es decir, el 50% central de los datos) es bastante amplio, desde ~15 hasta ~61 meses.
Hay valores mínimos de 0 meses (clientes con contratos muy cortos) y máximos hasta ~72 meses.
Esto sugiere que muchos de los clientes no vigentes tuvieron contratos relativamente largos antes de dejar de serlo.

Clientes Vigentes (1, en gris):
La mediana está alrededor de 10 meses, lo que indica que la mayoría llevan poco tiempo.
Su IQR es mucho más estrecho (~2 a ~29 meses).
Existen outliers (puntos fuera del rango esperado), pero en general el tiempo es más corto que en los no vigentes.
Esto sugiere que muchos de los clientes vigentes son relativamente nuevos.

**Conclusión del informe:**

El tiempo de contrato difiere considerablemente entre los clientes vigentes y no vigentes. 
Los clientes no vigentes tienden a haber tenido relaciones contractuales más largas, mientras que los clientes vigentes se concentran en duraciones más cortas, lo que podría indicar que son nuevos o que existe una rotación significativa en los primeros años de contrato.

**Finalmente:**
🧩 Este análisis en la compañia TelecomX_LTAM puede servir para: Identificar perfiles de riesgo (clientes nuevos y de bajo gasto). Diseñar estrategias de retención más dirigidas.

Realizado por: Starleen Gaviria Medina, Estudiante de Alura Latam, Ciencia de datos.

www.linkedin.com/in/starleen-gaviria-sig
