# Uso de autoencoders para la detección de anomalías en tráfico web

## Descripción general
Este proyecto implementa un modelo de Aprendizaje Profundo basado en Autoencoders con redes LSTM para la detección de anomalías en series temporales de tráfico web. El sistema aprende el comportamiento normal del tráfico diario de múltiples páginas web y detecta picos o caídas atípicas a partir del error de reconstrucción generado por el modelo entrenado.

El desarrollo corresponde a un proyecto final de la materia Redes Neuronales y Aprendizaje Profundo y fue realizado utilizando Google Colab como entorno de ejecución, con soporte para aceleración por GPU y almacenamiento persistente mediante Google Drive. Los datos utilizados son reales y se encuentran en formato TSF (Time Series Forecasting).

## Objetivo del proyecto
El objetivo general del proyecto es desarrollar un sistema no supervisado capaz de identificar comportamientos anómalos en series temporales de tráfico web. El modelo busca aprender patrones normales a partir de múltiples series, sin requerir etiquetas previas, y generar visualizaciones que permitan interpretar de forma clara los periodos considerados atípicos.

## Alcance y características
El proyecto utiliza un Autoencoder LSTM entrenado de manera global con múltiples series temporales. El sistema realiza un escalado conjunto de los datos, genera ventanas temporales para el entrenamiento, calcula un umbral estadístico de anomalía y produce automáticamente gráficas y archivos de salida que documentan los resultados obtenidos. El diseño permite ejecutar el proyecto tanto en CPU como en GPU, siendo esta última opción preferible para reducir tiempos de entrenamiento.

## Estructura del proyecto
La organización del proyecto se basa en una carpeta principal que contiene el dataset, el código fuente y los resultados generados durante la ejecución. La estructura general del proyecto es la siguiente:

```text
RN_Proyecto/
│
├── kaggle_web_traffic_dataset.tsf
│
├── Salidas_multi/
│   ├── historial_entrenamiento_global.csv
│   ├── anomalias_serie_0.png
│   ├── anomalias_serie_1.png
│   ├── ...
│
└── ProyectoRedes.ipynb
   └── proyectoredes.py

```

## Dataset
El conjunto de datos utilizado corresponde a series temporales reales de tráfico web, donde cada serie representa el número de visitas diarias a una página. El archivo se encuentra en formato TSF, el cual incluye metadatos y una sección de datos que contiene las series completas. Durante el preprocesamiento, los valores faltantes se manejan mediante su reemplazo por cero con el objetivo de mantener la continuidad temporal de las series.

## Requisitos del sistema
El proyecto fue ejecutado en Google Colab, utilizando un entorno virtual con CPU Intel Xeon y aproximadamente entre doce y quince gigabytes de memoria RAM. Cuando estuvo disponible, se utilizó una GPU NVIDIA proporcionada por Colab para acelerar el proceso de entrenamiento. A nivel de software, el sistema requiere Python, TensorFlow con Keras, NumPy, Pandas, Matplotlib y Scikit-learn, además del acceso a Google Drive para el almacenamiento de datos y resultados.

## Arquitectura del modelo
La arquitectura implementada corresponde a un Autoencoder LSTM compuesto por dos capas LSTM que actúan como codificador y una parte densa que permite reconstruir el valor de salida. La primera capa LSTM utiliza ciento veintiocho unidades y devuelve secuencias completas, mientras que la segunda capa utiliza sesenta y cuatro unidades. Posteriormente se emplea una capa densa intermedia con función de activación ReLU y una capa final que produce el valor reconstruido. El modelo se entrena utilizando el error cuadrático medio como función de pérdida y el optimizador Adam.

## Funcionamiento del sistema
El flujo de funcionamiento comienza con la carga del dataset desde Google Drive y la lectura del archivo TSF. A continuación se selecciona un subconjunto de series para el entrenamiento global del modelo. Los datos se escalan de forma conjunta y se transforman en ventanas temporales de longitud fija. El Autoencoder LSTM se entrena con estas ventanas y posteriormente se calcula el error de reconstrucción para cada una. A partir de la distribución de estos errores se define un umbral estadístico que permite identificar las anomalías. Finalmente, el sistema genera y guarda automáticamente las gráficas correspondientes a cada serie.

## Pruebas y resultados
Durante la ejecución del proyecto se obtienen diversos resultados que permiten evaluar el desempeño del modelo. Se genera un historial de entrenamiento que muestra la evolución de la función de pérdida a lo largo de las épocas, el cual se guarda en formato CSV. Asimismo, se producen gráficas donde se visualiza el tráfico real de cada serie junto con los puntos identificados como anomalías. Estos resultados permiten analizar de forma visual y cuantitativa el comportamiento del modelo.

## Ejecución del proyecto
Para ejecutar el proyecto es necesario colocar el archivo TSF en la ruta correspondiente dentro de Google Drive y abrir el notebook o script en Google Colab. En caso de requerir aceleración por hardware, se debe habilitar la GPU desde la configuración del entorno de ejecución. Una vez configurado el entorno, el proyecto puede ejecutarse de principio a fin sin requerir configuraciones adicionales.

## Código y apéndice
El código completo del proyecto se encuentra documentado y organizado en el archivo del notebook y en su versión en Python. Este código incluye todas las etapas del proceso, desde la lectura del dataset hasta la generación de resultados y gráficas, y está preparado para ser incluido como apéndice en el documento final del proyecto.

## Referencias
El desarrollo del proyecto se apoya en bibliografía clásica de aprendizaje profundo, artículos relacionados con el uso de Autoencoders y LSTM para detección de anomalías en series temporales, así como en la documentación oficial de TensorFlow y Keras y en fuentes públicas de datasets en formato TSF.
<br>
**Autores:** Axel Jair Segundo León, Luis Gerardo Gallegos Pérez <br>
**Dataset:** https://www.kaggle.com/c/web-traffic-time-series-forecasting <br>
**Link alternativo para dataset:** https://zenodo.org/records/4656075

