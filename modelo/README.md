# Análisis de emociones con 6 lineas de código
[fuente](https://medium.com/qu4nt/an%C3%A1lisis-de-sentimientos-en-espa%C3%B1ol-con-seis-l%C3%ADneas-de-c%C3%B3digo-2d21cf82b7b4)

Sin más preámbulos, aquí va el código:

```python
from transformers import pipeline

emotion_analysis = pipeline("sentiment-analysis",
                            model="pysentimiento/robertuito-emotion-analysis")

sentiment_analysis = pipeline("sentiment-analysis",
                       model="BramVanroy/bert-base-multilingual-cased-hebban-reviews",)
```

El resultado es una clasificación de análisis de sentimientos y emociones para cada cadena de la lista sentences:

```python
result1 = sentiment_analysis("Esta pelicula es horrible")
result1
```
```
[{'label': 'negative', 'score': 0.9272792935371399}]
```

```python
result2 = emotion_analysis("Maldita sea esta película")
result2
```
```
[{'label': 'anger', 'score': 0.6421485543251038}]
```

Y eso es todo. Para ponerlo a funcionar debes instalar en tu sistema (con pip o conda) la librería transformers, así:

```python
$ pip install transformers
```

## La explicación

En el código de más arriba hemos utilizado una librería impresionante denominada 🤗 Transformers (sí, así mismo, con el emoji y todo) y que forma parte del proyecto de HuggingFace. Te recomiendo que te des un paseo por esa comunidad que está haciéndonos la vida mucho más fácil a quienes estamos interesados en la Inteligencia Artificial, y en particular a los que trabajamos con Procesamiento de Lenguaje Natural.

La gente de HuggingFace ha puesto en un único sitio un buen número de modelos de Deep Learning entrenados para tareas de NLP, además de una gran cantidad de datasets en varios idiomas. Y no contentos con eso han desarrollado un API que te permite, como en el ejemplo de arriba, utilizar tecnología de punta con unas pocas líneas de código.

El código funciona para hacer análisis de sentimientos (sentiment analysis) en español — utiliza un modelo llamado Bert-base entrenado específicamente para el análisis de sentimientos — , pero es multiidioma, así que también lo puedes utilizar para el inglés, francés, holandés, italiano y alemán.
