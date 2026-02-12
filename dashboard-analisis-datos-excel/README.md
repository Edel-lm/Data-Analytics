
Análisis Multidimensional de Ventas, Rentabilidad y Segmentación en el Global Superstore Dataset

1.	Descripción del proyecto
Este proyecto desarrolla un análisis estratégico de datos comerciales con el objetivo de identificar patrones de ventas, desempeño por mercado, rentabilidad por producto y segmentación de clientes. 
A través de un proceso de limpieza, transformación y análisis descriptivo de datos, se construye un dashboard interactivo en Excel que permite visualizar indicadores clave de negocio y facilitar la toma de decisiones basada en datos.
2.	Estructura del proyecto
El repositorio se organiza de la siguiente manera:

├── data/  
│   └── global_superstore_original.csv        # Dataset original descargado de Kaggle (sin modificaciones)  

├── dashboard/  
│   └── analisis_superstore.xlsx              # Archivo único de Excel que contiene todo el proceso de limpieza, análisis y dashboard  

├── README.md                                 # Documentación del proyecto e informe del análisis  

### Descripción de los archivos

- global_superstore_original.csv: Archivo con los datos originales tal y como fueron descargados desde Kaggle. Se conserva sin modificaciones para garantizar trazabilidad y reproducibilidad del análisis.

- analisis_superstore.xlsx: Archivo principal de trabajo que incluye:
  - Proceso de limpieza y transformación de datos.
  - Creación de variables derivadas (año, semana, métricas agregadas, etc.).
  - Análisis descriptivo mediante tablas dinámicas.
  - Construcción del dashboard final con indicadores clave de negocio.

3.	Metodología y Limpieza de Datos
El proceso de preparación del dataset se desarrolló en varias fases con el objetivo de garantizar la integridad estructural y la calidad analítica de los datos antes de su exploración y visualización.
3.1.	Importación y Preprocesamiento Estructural
El archivo original descargado desde Kaggle (global_superstore_original.csv) presentaba inconsistencias en su serialización CSV, incluyendo:
- Comillas escapadas dobles (`""`).
- Comillas externas envolviendo cada fila.
- Presencia de delimitadores finales adicionales (`";`).
- Comas internas dentro de nombres de productos.
Estas características impedían que Excel interpretara correctamente las columnas utilizando el asistente estándar de importación.
Para resolverlo sin modificar el archivo original (manteniendo trazabilidad), se realizó un preprocesamiento estructural en Power Query para corregir problemas de serialización del archivo CSV y garantizar una correcta delimitación de columnas, manteniendo el archivo original sin modificaciones
Este procedimiento permitió obtener correctamente las 26 columnas del dataset sin desplazamientos ni pérdida de información.
3.2.	Conversión y Validación de Tipos de Datos
Una vez estructurado el dataset, se procedió a:
- Conversión de variables temporales (“Order.Date”, “Ship.Date”) al formato fecha.
- Conversión de variables numéricas (“Sales”, “Profit”, “Shipping.Cost”, “Discount”, “Quantity”) al tipo numérico adecuado.
- Revisión de coherencia en identificadores (“Order.ID”, “Customer.ID”, “Product.ID”).
3.3.	Tipificación de Variables
Tras la limpieza estructural del archivo, todas las columnas fueron inicialmente interpretadas como texto. 
Se realizó una tipificación manual de las variables en Power Query, clasificándolas en:

- Variables categóricas (Texto): Category, Segment, Region, City, Country, Product.Name, entre otras.
- Variables numéricas (Número decimal / entero): Sales, Profit, Shipping.Cost, Discount, Quantity, Year, weeknum.
- Variables temporales (Fecha): Order.Date y Ship.Date.
Para las variables numéricas con formato anglosajón (separador decimal con punto), se utilizó la opción "Usar configuración regional" con configuración Inglés (Estados Unidos), garantizando la correcta interpretación de los valores.

3.4.	Eliminación de Variables No Relevantes
Se eliminó la columna “记录数”, correspondiente a un contador constante (valor igual a 1 en todos los registros), ya que no aportaba información analítica relevante y resultaba redundante para el modelo de datos.

3.5.	Auditoría de Calidad de Datos
Se realizó una revisión sistemática del dataset mediante herramientas de perfilado en Power Query (calidad, distribución y perfil de columnas), evaluando la presencia de valores nulos, errores de conversión y posibles inconsistencias.
Durante esta fase se identificaron 7 registros con errores o valores nulos en múltiples variables clave (Sales, Profit, Segment y Region), representando menos del 0,02% del total de observaciones.
Dado su carácter residual y su impacto estadísticamente irrelevante, se procedió a su eliminación para garantizar la consistencia del análisis posterior.
El dataset final quedó compuesto por 51.284 registros válidos.

4. Preparación Analítica del modelo
4.1. Creación de Variables Derivadas
Con el objetivo de enriquecer el análisis y facilitar la construcción del dashboard, se generaron nuevas variables analíticas a partir de las columnas originales:

-	Month_Num: Número de mes extraído de “Order.Date”, para permitir análisis temporal estructurado.
-	Month: Nombre del mes para visualización en gráficos.
-	Margin_%: Calculado como `Profit / Sales`, con el fin de analizar la rentabilidad relativa.
-	Shipping_Days: Diferencia entre “Ship.Date” y “Order.Date”, permitiendo evaluar la eficiencia logística.
-	Profit_Status: Variable categórica que clasifica cada transacción como “Profitable” o “Unprofitable” en función del signo del beneficio.

Estas variables permitieron realizar un análisis más profundo en dimensiones temporal, financiera y operativa.

5.	Análisis Descriptivo
Una vez preparado el modelo de datos, se procedió al análisis descriptivo utilizando tablas dinámicas y visualizaciones en Excel.
El análisis se estructuró en distintas dimensiones con el objetivo de obtener una visión global del rendimiento del negocio.
5.1.	KPIs Generales
Se construyeron indicadores clave de rendimiento (KPIs) a partir de agregaciones mediante tablas dinámicas:
-	Total Sales
-	Total Profit
-	Total Quantity
-	Total Orders (recuento distinto de Order.ID)
-	Real Margin %
El margen global fue calculado como:
= Total Profit / Total Sales
Se evitó el uso del promedio simple de márgenes individuales, garantizando así una medida financiera correcta y representativa.
5.2.	Análisis Temporal
Se analizó la evolución de ventas y beneficio por año mediante un gráfico combinado (columnas para ventas y línea para beneficio).
Se observó una tendencia de crecimiento sostenido entre 2011 y 2014, con una evolución paralela entre ventas y beneficio, lo que sugiere estabilidad en la rentabilidad global.

5.3.	Análisis Geográfico
Se evaluó el desempeño por región mediante gráficos de barras.
Los resultados muestran una fuerte concentración del negocio en determinadas regiones, destacando:
-	Central como principal mercado en volumen de ventas y beneficio.
-	Diferencias significativas entre regiones en términos de contribución al resultado global.
A partir de este análisis se identificó la dependencia geográfica del negocio y posibles oportunidades de mejora en regiones con menor rentabilidad relativa.
5.4.	Análisis por Categoría
Se analizó el desempeño de las distintas categorías de producto mediante tablas dinámicas y gráficos de columnas agrupadas, evaluando tanto el volumen de ventas como el beneficio generado.
Aunque la categoría con mayor volumen de ventas también lidera en beneficio absoluto, se observan diferencias significativas en la relación entre ventas y rentabilidad relativa. 
Este análisis permitió identificar que el volumen no siempre implica mayor eficiencia financiera, haciendo necesario evaluar el margen por categoría para obtener una visión más precisa de la rentabilidad.
5.5.	Análisis por Subcategoría
Se profundizó en el análisis evaluando la rentabilidad a nivel de subcategoría.
Mediante gráficos de barras horizontales ordenados por beneficio, se identificaron subcategorías altamente rentables y otras con bajo desempeño o incluso pérdidas.

Este análisis permitió detectar:

- Subcategorías con alto beneficio y menor volumen.
- Subcategorías con alto volumen pero bajo margen.
- Casos con beneficio negativo, que podrían indicar problemas de estructura de costes o política de descuentos.
Este nivel de detalle aporta información clave para la toma de decisiones estratégicas sobre el portfolio de productos.
5.6.	Impacto del Descuento en la Rentabilidad
Se analizó la relación entre el nivel de descuento aplicado y el beneficio generado.
Agrupando los descuentos por tramos, se construyó un gráfico combinado que permitió observar la evolución del beneficio en función del descuento.
Se evidenció una relación inversa entre descuento y rentabilidad: a medida que aumenta el nivel de descuento, el beneficio tiende a disminuir significativamente, especialmente en tramos superiores.
Este hallazgo sugiere que políticas de descuento agresivas pueden comprometer la rentabilidad del negocio.
5.7.	Análisis por Segmento de Cliente
Finalmente, se evaluó el desempeño por segmento de cliente (Consumer, Corporate y Home Office), comparando volumen de ventas y beneficio.
Este análisis permitió identificar el peso relativo de cada segmento en la estructura del negocio y evaluar su contribución al resultado global.
Se incorporaron segmentadores interactivos (Year, Region y Segment), permitiendo un análisis dinámico del desempeño bajo distintos filtros.
6.	Dashboard
Con el objetivo de sintetizar los principales hallazgos del análisis, se diseñó un dashboard interactivo en Excel estructurado en tres niveles: indicadores clave, análisis dimensional y segmentación dinámica.
6.1.	Indicadores Clave (KPIs)
En la parte superior del dashboard se incorporaron los siguientes KPIs:

-	Total Sales
-	Total Profit
-	Real Margin %
-	Total Orders
-	Total Quantity

El margen global fue calculado como el cociente entre beneficio total y ventas totales, garantizando una medida financiera precisa.
Estos indicadores permiten obtener una visión ejecutiva inmediata del desempeño general del negocio.

6.2.	Análisis Dimensional
El dashboard incluye visualizaciones estructuradas en distintas dimensiones:
- Evolución temporal de ventas y beneficio por año.
- Desempeño geográfico por región.
- Rentabilidad por categoría y subcategoría.
- Impacto del nivel de descuento en la rentabilidad.
- Comparativa por segmento de cliente.
Las visualizaciones fueron diseñadas priorizando claridad, jerarquía visual y coherencia cromática.

6.3.	Interactividad
Se incorporaron segmentadores (Year, Region y Segment) que permiten filtrar dinámicamente todas las visualizaciones del dashboard.
Esto facilita el análisis exploratorio y permite evaluar el desempeño del negocio bajo distintos escenarios.
El diseño del dashboard sigue una estructura limpia y profesional, separando la capa de datos, la capa de cálculo y la capa de visualización, garantizando escalabilidad y claridad analítica.

7.	Conclusiones

El análisis del dataset Global Superstore ha permitido obtener una visión integral del desempeño comercial, financiero y operativo del negocio.

Crecimiento Sostenido
Se observa una tendencia de crecimiento continuo en ventas y beneficio entre 2011 y 2014, manteniendo una evolución paralela que indica estabilidad en la rentabilidad global.
Concentración Geográfica
El negocio presenta una fuerte concentración en determinadas regiones, especialmente Central, que lidera tanto en volumen de ventas como en beneficio. 
Existen regiones con menor peso relativo que podrían representar oportunidades de expansión o mejora en eficiencia.
Diferencias de Rentabilidad por Producto
Aunque algunas categorías y subcategorías generan alto volumen de ventas, no todas presentan la misma eficiencia en términos de margen.
Se identificaron subcategorías altamente rentables (como Copiers) y otras con bajo desempeño o pérdidas (como Tables), lo que sugiere posibles ajustes en estrategia de precios, costes o posicionamiento.
Impacto del Descuento en el Beneficio
El análisis muestra una relación inversa entre nivel de descuento y rentabilidad. A medida que aumenta el descuento, el beneficio tiende a disminuir significativamente, especialmente en tramos elevados.
Esto sugiere que políticas de descuento agresivas pueden comprometer la rentabilidad del negocio si no están adecuadamente controladas.
Segmentación de Clientes
El segmento Consumer concentra la mayor parte del volumen de negocio, aunque el análisis comparativo permite evaluar la contribución relativa de Corporate y Home Office en términos de rentabilidad.
El uso de segmentadores interactivos facilita la evaluación dinámica del desempeño bajo distintos escenarios.
Conclusión General
El negocio presenta un crecimiento sólido y estructuralmente rentable, aunque existen áreas específicas (subcategorías con pérdidas y descuentos elevados) donde podrían implementarse estrategias de optimización para mejorar la eficiencia financiera.
El dashboard desarrollado permite monitorear estas dimensiones de forma dinámica y estructurada, facilitando la toma de decisiones basada en datos.
