# Análisis Multidimensional de Ventas, Rentabilidad y Segmentación en el Global Superstore Dataset

---

## 1. Descripción del proyecto

Este proyecto desarrolla un análisis estratégico de datos comerciales con el objetivo de identificar patrones de ventas, desempeño por mercado, rentabilidad por producto y segmentación de clientes.

A través de un proceso de limpieza, transformación y análisis descriptivo de datos, se construye un dashboard interactivo en Excel que permite visualizar indicadores clave de negocio y facilitar la toma de decisiones basada en datos.

---

## 2. Estructura del proyecto

El repositorio se organiza de la siguiente manera:

├── data/  
│   └── global_superstore_original.csv        # Dataset original descargado de Kaggle (sin modificaciones)  

├── dashboard/  
│   └── analisis_superstore.xlsx              # Archivo único de Excel que contiene todo el proceso de limpieza, análisis y dashboard  

├── README.md                                 # Documentación del proyecto e informe del análisis  

### Descripción de los archivos

**global_superstore_original.csv**  
Archivo con los datos originales descargados desde Kaggle. Se conserva sin modificaciones para garantizar trazabilidad y reproducibilidad.

**analisis_superstore.xlsx**  
Archivo principal que incluye:

- Proceso de limpieza y transformación
- Creación de variables derivadas
- Análisis descriptivo con tablas dinámicas
- Construcción del dashboard final

---

## 3. Metodología y Limpieza de Datos

El proceso de preparación del dataset se desarrolló en varias fases para garantizar la integridad estructural y la calidad analítica.

### 3.1 Importación y Preprocesamiento Estructural

El archivo CSV original presentaba:

- Comillas escapadas dobles ("")
- Comillas externas envolviendo cada fila
- Delimitadores finales adicionales
- Comas internas dentro de nombres de productos

Se realizó un preprocesamiento estructural en Power Query para corregir la serialización sin modificar el archivo original.

Se obtuvieron correctamente las 26 columnas del dataset.

---

### 3.2 Conversión y Validación de Tipos de Datos

- Conversión de variables temporales a formato fecha.
- Conversión de variables numéricas al tipo adecuado.
- Revisión de coherencia en identificadores.

---

### 3.3 Tipificación de Variables

Se clasificaron las variables en:

- **Categóricas:** Category, Segment, Region, City, Country, Product.Name.
- **Numéricas:** Sales, Profit, Shipping.Cost, Discount, Quantity, Year, weeknum.
- **Temporales:** Order.Date y Ship.Date.

Para las variables numéricas con formato anglosajón se utilizó configuración regional Inglés (Estados Unidos).

---

### 3.4 Eliminación de Variables No Relevantes

Se eliminó la columna “记录数”, ya que representaba un contador constante sin valor analítico.

---

### 3.5 Auditoría de Calidad de Datos

Se realizó perfilado de calidad en Power Query.

Se identificaron 7 registros con errores o valores nulos (<0,02%), que fueron eliminados.

El dataset final quedó compuesto por **51.284 registros válidos**.

---

## 4. Preparación Analítica del Modelo

### 4.1 Creación de Variables Derivadas

Se generaron nuevas variables:

- **Month_Num**
- **Month**
- **Margin_% = Profit / Sales**
- **Shipping_Days**
- **Profit_Status**

Estas variables permitieron ampliar el análisis temporal, financiero y operativo.

---

## 5. Análisis Descriptivo

### 5.1 KPIs Generales

Se construyeron los siguientes indicadores:

- Total Sales
- Total Profit
- Total Quantity
- Total Orders (recuento distinto)
- Real Margin %

El margen global fue calculado como:

= Total Profit / Total Sales
---

### 5.2 Análisis Temporal

Se analizó la evolución de ventas y beneficio entre 2011 y 2014, observando crecimiento sostenido y estabilidad en la rentabilidad.

---

### 5.3 Análisis Geográfico

Se evaluó el desempeño por región.

Destaca:

- Central como principal mercado.
- Dependencia geográfica significativa.

---

### 5.4 Análisis por Categoría

Se identificaron diferencias relevantes entre volumen de ventas y rentabilidad relativa.

El volumen no siempre implica mayor eficiencia financiera.

---

### 5.5 Análisis por Subcategoría

Se identificaron:

- Subcategorías altamente rentables (Copiers).
- Subcategorías con pérdidas (Tables).
- Diferencias significativas en eficiencia financiera.

---

### 5.6 Impacto del Descuento en la Rentabilidad

Se observó una relación inversa entre descuento y beneficio.

Descuentos elevados reducen significativamente la rentabilidad.

---

### 5.7 Análisis por Segmento de Cliente

Se compararon Consumer, Corporate y Home Office.

Se incorporaron segmentadores dinámicos (Year, Region, Segment).

---

## 6. Dashboard

El dashboard se estructuró en tres niveles:

### 6.1 Indicadores Clave

- Total Sales
- Total Profit
- Real Margin %
- Total Orders
- Total Quantity

---

### 6.2 Análisis Dimensional

Incluye visualizaciones por:

- Año
- Región
- Categoría
- Subcategoría
- Descuento
- Segmento

---

### 6.3 Interactividad

Se incorporaron segmentadores conectados a todas las visualizaciones.

Se separaron capa de datos, cálculo y visualización.

---

## 7. Conclusiones

### Crecimiento Sostenido

Evolución positiva entre 2011 y 2014.

### Concentración Geográfica

Fuerte dependencia de la región Central.

### Diferencias por Producto

Existen subcategorías con pérdidas que requieren revisión estratégica.

### Impacto del Descuento

Descuentos elevados reducen la rentabilidad.

### Segmentación

Consumer lidera en volumen, aunque la rentabilidad varía por segmento.

### Conclusión General

El negocio presenta crecimiento sólido y estructura rentable, aunque existen áreas de mejora en política de descuentos y optimización del portfolio.
