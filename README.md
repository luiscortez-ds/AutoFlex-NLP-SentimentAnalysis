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
