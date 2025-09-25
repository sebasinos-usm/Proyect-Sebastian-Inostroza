# CLASIFICADOR DE INFORMES RADIOLOGICOS CRITICOS CON USO DE IA ML
# Proyect Sebastian Inostroza - USM - DIPLOMADO IA EN SALUD

## RESUMEN ELECCION DEL PROBLEMA ##
La generación diaria de estudios de imagenología ha resultado en un aumento exponencial del volumen de informes radiológicos, presentando un desafío operativo para su revisión oportuna y priorizada. En este escenario, la correcta identificación de 
"Resultados Críticos" aquellos que requieren comunicación urgente con el médico tratante— es un pilar para la seguridad del paciente. Sin embargo, la variabilidad de criterios entre distintos centros y protocolos puede llevar a inconsistencias en esta tarea crucial.
Para abordar este desafío, el presente proyecto se centra en el desarrollo de un modelo de inteligencia artificial como herramienta de apoyo clínico. El objetivo principal es crear un sistema capaz de leer y analizar el texto de los informes radiológicos para sugerir su clasificación como "crítico" o "no crítico". Lejos de reemplazar el juicio del especialista, esta herramienta busca ofrecer una segunda opinión sistemática y estandarizada, reforzando el criterio del radiólogo y aportando a la homogeneización de los protocolos institucionales.

## POR TEMAS DE PRIVACIDAD DE DATOS SOLO SE COMPARTE EL DATASET YA ANONIMIZADO. POR LO QUE SOLO SE EXPLICA Y SE COMPARTE CODIGO DE COMO SE PROCESARON LOS ARCHIVOS ORIGINALES.

# Clasificador de Informes Radiológicos Basado en Criticidad

Este proyecto utiliza técnicas de Procesamiento del Lenguaje Natural (NLP) y Machine Learning para clasificar automáticamente informes radiológicos médicos como "Críticos" o "No Críticos". El objetivo principal es desarrollar una herramienta que ayude a Radiologos a la toma de desicion y revision retrospectiva para Aalisis de Calidad, optimizando el flujo de trabajo de los profesionales de la salud.

## 📜 Descripción del Proyecto

El sistema se entrena con un conjunto de informes en formato PDF, previamente etiquetados. A través de un pipeline de procesamiento de datos, los informes son extraídos, limpiados, anonimizados y transformados en un formato numérico (TF-IDF) para alimentar a los modelos de clasificación. Se entrenan y comparan dos modelos (Regresión Logística y Naive Bayes), seleccionando el más adecuado en función de métricas clave para el contexto médico, como la reducción de Falsos Negativos.

## ✨ Características Principales

- **Pipeline Completo de Datos:** Un flujo de trabajo de extremo a extremo que convierte informes PDF en datos limpios y listos para el modelo.
- **Procesamiento de Texto Avanzado:** Incluye extracción de texto desde PDF conversion a TXT, eliminación de duplicados, anonimización por bloques y limpieza de texto estándar (stopwords, acentos, etc.).
- **Entrenamiento y Evaluación de Modelos:** Entrena y evalúa modelos de `Regresión Logística` y `Naive Bayes`, guardando el mejor modelo para su uso posterior.
- **Métricas de Evaluación Robustas:** Utiliza métricas como la Matriz de Confusión, Curva ROC-AUC, Curva PR y Recall@k para una evaluación completa y adecuada al problema.
- **Aplicación Final:** Incluye un script final para clasificar nuevos informes en PDF y obtener un diagnóstico de criticidad con su respectivo porcentaje de confianza.

## 🛠️ Tecnologías y Librerías Utilizadas

- **Python 3**
- **Jupyter Notebook**
- **Pandas y NumPy:** para la manipulación y análisis de datos.
- **Scikit-learn:** para el pipeline de Machine Learning (TF-IDF, modelos, métricas).
- **PyMuPDF (fitz):** para la extracción de texto desde archivos PDF.
- **NLTK:** para el preprocesamiento de texto en español (stopwords).
- **Matplotlib y Seaborn:** para la visualización de resultados.
- **Joblib:** para guardar y cargar los modelos entrenados.

## 📂 Estructura del Proyecto
/
├── Informes_pdf/              # (Opcional) Carpeta para los PDF originales (no incluida en Git).
├── Informes_Para_Testear/     # Carpeta donde se colocan los nuevos PDF a clasificar.
├── Proyecto_oficial.ipynb     # Notebook principal con todo el análisis y código.
├── pipeline_naive_bayes.pkl   # Modelo final entrenado y guardado.
├── Informes_Anonimizados/     # Carpeta con TXT anonimizados para entrenar el modelo.
└── README.md                  # Este archivo.

## 🚀 Flujo de Trabajo (Pipeline)

El proyecto sigue una secuencia de fases bien definida dentro del notebook:

1.  **Extracción de Texto:** Convierte los informes originales de formato PDF a archivos de texto (`.txt`), preservando el layout.
2.  **Limpieza de Duplicados:** Utiliza hashing (SHA-256) para identificar y descartar informes duplicados, asegurando la unicidad de los datos.
3.  **Anonimización:** Procesa los informes para eliminar datos sensibles y, lo más importante, aísla el cuerpo del informe usando marcadores textuales como "Examen:" y "Dr.".
4.  **Preprocesamiento NLP:** Aplica técnicas de limpieza de texto, como la conversión a minúsculas, eliminación de acentos, puntuación y stopwords.
5.  **Entrenamiento del Modelo:** Carga los datos procesados en un DataFrame, los vectoriza usando TF-IDF y entrena los modelos de clasificación.
6.  **Evaluación y Selección:** Evalúa los modelos y concluye que **Naive Bayes** es superior debido a su menor tasa de Falsos Negativos. Se optimiza aún más ajustando su **umbral de decisión a 0.4**.

## 📊 Resultados y Conclusiones

- El modelo **Naive Bayes** demostró ser más adecuado que la Regresión Logística para este problema, ya que **minimizó la cantidad de informes críticos no detectados** (8 Falsos Negativos vs. 12 de la Regresión Logística).
- La mejora más significativa se logró al **ajustar el umbral de decisión del modelo Naive Bayes a 0.4**. Esta optimización elevó la capacidad de detección (Recall) a un **95.8%**, asegurando que casi todos los casos críticos fueran identificados correctamente, a costa de un aumento aceptable en las falsas alarmas.

## ⚙️ Cómo Usar el Clasificador

Para clasificar nuevos informes, sigue estos pasos:

1.  **Requisitos Previos:** Asegúrate de tener Python y las librerías mencionadas instaladas. Puedes instalarlas con pip:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn pymupdf nltk joblib
    ```

2.  **Ejecución:**
    1.  Clona o descarga este repositorio.
    2.  Asegúrate de que el archivo `pipeline_naive_bayes.pkl` esté en la misma carpeta que el notebook.
    3.  Crea una carpeta llamada `Informes_Para_Testear`.
    4.  Coloca los nuevos informes en formato PDF que deseas analizar dentro de esa carpeta.
    5.  Abre el notebook `Proyecto_oficial.ipynb` y ejecuta la última celda de código, bajo la sección **"APLICACION FINAL - TESTEO DE NUEVOS INFORMES"**. Los resultados aparecerán en la salida de la celda.
