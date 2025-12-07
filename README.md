 Análisis de Sentimientos – AutoFlex (NLP)

Este proyecto aplica técnicas de Procesamiento de Lenguaje Natural (NLP) para analizar comentarios de clientes y clasificarlos en tres categorías principales:

bueno

malo

info (consultas o solicitudes de información)

El objetivo es comprender el contenido de los comentarios, visualizar sus patrones y entrenar un modelo capaz de clasificarlos automáticamente.

Incluye limpieza de texto, análisis exploratorio (EDA), visualizaciones y construcción de un modelo de clasificación usando TF-IDF.

 1. Preprocesamiento del texto (Limpieza Nivel B)

Se aplicó una limpieza intermedia, ideal para NLP:

Conversión a minúsculas

Eliminación de signos de puntuación

Tokenización

Remoción de stopwords en español

Conservación solo de palabras alfabéticas

def limpiar_texto(texto):
    texto = texto.lower()
    texto = texto.translate(str.maketrans("", "", string.punctuation))
    tokens = texto.split()
    tokens = [t for t in tokens if t.isalpha() and t not in stop_es]
    return " ".join(tokens)


Resultado esperado:
Se agrega la columna clean, con la versión procesada del texto original.

 2. Análisis Exploratorio (EDA)
 a) Wordcloud (Nube de Palabras)

Muestra las palabras más frecuentes en los comentarios procesados.

 b) Frecuencia de palabras (Top 15)

Gráfico con las palabras más repetidas después de la limpieza.

 c) Distribución por clase (target)

Cantidad de comentarios etiquetados como:
malo, info, bueno.

 3. Modelo de Machine Learning

Se implementó un pipeline clásico para clasificación de texto:

1. Vectorización con TF-IDF

Transforma el texto en una matriz numérica basada en la importancia de cada término.

2. Entrenamiento con RandomForestClassifier

Modelo robusto para clasificación inicial.

vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(df["clean"])
y = df["target"]

model = RandomForestClassifier()
model.fit(X_train, y_train)

Resultados del modelo

Detecta palabras clave que definen cada clase

Buen rendimiento con comentarios cortos

Clasifica adecuadamente textos de tipo info, que suelen ser muy frecuentes

 4. Insights del análisis

Los hallazgos principales del proyecto muestran que:

Los comentarios "malo" incluyen términos relacionados con problemas de crédito, falta de respuesta o desconfianza.

Los comentarios "info" representan usuarios interesados en obtener más detalles: alta intención de compra.

Los comentarios "bueno" destacan elementos positivos de estética o calidad, aunque son minoría.

Esto permite:

✔ Priorizar clientes que piden información
✔ Detectar rápidamente comentarios negativos
✔ Automatizar la clasificación de nuevos mensajes
✔ Comprender los temas principales que mencionan los usuarios
✔ Priorizar clientes que piden información
✔ Detectar rápidamente comentarios negativos
✔ Automatizar la clasificación de nuevos mensajes
✔ Comprender los temas principales que mencionan los usuarios

📁 Estructura del Repositorio

AutoFlex-NLP-SentimentAnalysis/
│── README.md
│── notebook.ipynb
│── data/
│   └── comentarios.csv
│── images/
    ├── wordcloud.png
    ├── palabras frecuentes.png
    └── distrubucion targetr.png

