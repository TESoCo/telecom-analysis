# Análisis ConnectaTel - Comportamiento de Clientes

## Descripción General

Este repositorio contiene el análisis de datos de **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica, con el objetivo de evaluar el comportamiento de sus clientes durante el año 2024. El análisis se centra en la exploración, limpieza y segmentación de los datos.

## Datasets Utilizados

El análisis se basa en tres conjuntos de datos que se cargan desde la carpeta "/datasets/":

-   **"plans.csv"**: Contiene información sobre los planes actuales de la compañía, incluyendo precios, minutos y GB incluidos, y costos por exceso.
-   **"users_latam.csv"**: Almacena información demográfica y de registro de los clientes (edad, ciudad, fecha de registro, plan) y su estado en la empresa ("churn_date").
-   **"usage.csv"**: Proporciona un detalle del uso real de los servicios por parte de los clientes, con registros de llamadas y mensajes de texto.

## Etapas del Análisis

El proyecto se estructura en las siguientes fases clave, documentadas en el notebook:

1.  **Carga y Exploración Inicial:**
    -   Importación de librerías (pandas, numpy, seaborn, y matplotlib).
    -   Carga de los tres datasets y visualización de las primeras filas para entender su estructura.
    -   Inspección de tipos de datos y dimensiones de cada DataFrame.

2.  **Identificación de Problemas de Calidad de Datos:**
    -   Valores Nulos: Cuantificación y análisis de valores faltantes en "users" y "usage". Se determinó que los nulos en "duration" y "length" son estructurales (MAR) y deben mantenerse.
    -   Valores Inválidos y Sentinels: Detección de valores atípicos como "-999" en "age" y "?" en "city", que fueron tratados como datos faltantes.
    -   Fechas: Análisis de las columnas de fecha ("reg_date", "date"), identificando y marcando como nulas las fechas futuras (posteriores a 2024).

3.  **Limpieza de Datos:**
    -   Reemplazo del sentinel "-999" en "age" por la mediana de la columna.
    -   Sustitución del sentinel "?" en "city" por "pd.NA".
    -   Marcación de fechas de registro futuras como valores nulos ("pd.NaT").

4.  **Resumen de Uso por Usuario:**
    -   Agregación de la tabla "usage" por usuario para calcular métricas clave: número total de llamadas, mensajes y minutos de llamada.
    -   Creación de un perfil de usuario unificado ("user_profile") al combinar los datos agregados con el dataset "users".

5.  **Análisis Exploratorio y Visualización:**
    -   Cálculo de estadísticas descriptivas para variables numéricas ("age", "cant_mensajes", etc.) y distribución porcentual del tipo de plan.
    -   Creación de histogramas para visualizar la distribución de edades, cantidad de mensajes, llamadas y minutos de llamada. Se observó que las métricas de uso tienden a estar sesgadas a la derecha.
    -   Uso de boxplots para la identificación visual de outliers en las variables de uso y demográficas.

6.  **Segmentación de Clientes:**
    -   **Segmentación por Uso:** Clasificación de clientes en tres grupos ("Bajo uso", "Uso medio", "Alto uso") basados en la cantidad de llamadas y mensajes.
    -   **Segmentación por Edad:** Clasificación de clientes en tres grupos ("Joven", "Adulto", "Adulto mayor") según su rango de edad.

## Cómo Ejecutar el Notebook

1.  **Abrir en Google Colab:**
    -   Sube el archivo ".ipynb" a tu Google Drive.
    -   Haz clic derecho sobre el archivo, selecciona "Abrir con" y elige "Google Colaboratory".

2.  **Alternativa: Subir a GitHub y abrir desde Colab:**
    -   Sube el notebook a un repositorio en GitHub.
    -   En Google Colab, ve a "Archivo > Abrir notebook > GitHub" y pega la URL de tu repositorio.

3.  **Ejecutar las Celdas:**
    -   Asegúrate de tener los tres archivos CSV ("plans.csv", "users_latam.csv", "usage.csv") en una carpeta llamada "datasets/" en la raíz del entorno de Colab.
    -   Ejecuta las celdas del notebook en orden secuencial haciendo clic en el botón de "Play" o usando "Shift + Enter".

## Guía de Reproducción

Para reproducir este análisis desde cero, sigue estos pasos:

1.  **Configuración del Entorno:**
    -   Abre el notebook en un entorno que soporte Python 3 y las librerías necesarias (Colab, Jupyter Notebook, etc.).
    -   Asegúrate de que los archivos de datos ("plans.csv", "users_latam.csv", "usage.csv") estén en la ruta correcta especificada en el paso 1 del notebook ("/datasets/").

2.  **Ejecución Secuencial:**
    -   Sigue el orden de las secciones del notebook (Paso 1 a Paso 7).
    -   Cada sección de código está diseñada para ser ejecutada en orden, ya que los resultados de un paso son a menudo la entrada para el siguiente.
    -   Lee los comentarios y las celdas de Markdown para entender el propósito de cada bloque de código.

3.  **Análisis de Resultados:**
    -   Los insights generados después de cada gráfico contienen las conclusiones clave del análisis.
    -   La sección final, "Insight Ejecutivo", resume los hallazgos más importantes y las recomendaciones para el negocio.

---

**Autor:** José Taylor

**Fecha:** Noviembre 2026
