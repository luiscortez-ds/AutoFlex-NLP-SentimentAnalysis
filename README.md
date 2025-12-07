# AutoFlex-NLP-SentimentAnalysis
Análisis de sentimientos utilizando NLP para AutoFlex (Python + EDA + Wordclouds + Clasificación básica)

# Análisis de Sentimientos – AutoFlex (NLP)

Este proyecto aplica técnicas de **Procesamiento de Lenguaje Natural (NLP)** para analizar comentarios provenientes de clientes y clasificarlos en tres categorías:

- **bueno**  
- **malo**  
- **info** (consultas o solicitudes de información)

El flujo incluye limpieza de texto, análisis exploratorio (EDA), visualizaciones y construcción de un modelo de clasificación utilizando TF-IDF.

---

# 🧹 1. Preprocesamiento del texto

Se aplicó una limpieza de nivel intermedio:

- Conversión a minúsculas  
- Eliminación de puntuación  
- Tokenización  
- Remoción de *stopwords* en español  
- Conservación únicamente de palabras alfabéticas  

```python
def limpiar_texto(texto):
    texto = texto.lower()
    texto = texto.translate(str.maketrans("", "", string.punctuation))
    tokens = texto.split()
    tokens = [t for t in tokens if t.isalpha() and t not in stop_es]
    return " ".join(tokens)

# 🔎 2. Análisis Exploratorio (EDA)

📌 a) Wordcloud (Nube de Palabras)

Muestra las palabras más frecuentes en los comentarios procesados.

📌 b) Frecuencia de palabras (Top 15)

Gráfico con las palabras más repetidas después de la limpieza.

📌 c) Distribución por clase (target)

Cantidad de comentarios etiquetados como:
malo, info, bueno.

# 3. Modelo de Machine Learning

Se implementó un pipeline clásico para clasificación de texto:

1. Vectorización con TF-IDF

Transforma el texto en una matriz numérica basada en importancia de términos.

2. Entrenamiento con RandomForestClassifier

Modelo robusto para clasificación inicial.

Código simplificado:
vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(df["clean"])
y = df["target"]

model = RandomForestClassifier()
model.fit(X_train, y_train)

Resultados del modelo:

Detecta palabras clave que definen cada clase

Muy buen rendimiento con comentarios cortos

Clasifica adecuadamente textos de tipo info, que suelen ser más comunes

# 4. Insights del análisis

Los hallazgos principales del proyecto muestran que:

Los comentarios malo incluyen términos relacionados con problemas de crédito, falta de confianza o respuestas tardías.

Los comentarios info representan usuarios interesados en obtener más detalles: alta intención de compra.

Los comentarios bueno destacan elementos positivos de estética o calidad, aunque son minoría.

Esto permite:

✔ Priorizar clientes que piden información
✔ Detectar rápidamente comentarios negativos
✔ Automatizar la clasificación de nuevos mensajes
✔ Comprender los temas principales que mencionan los usuarios
