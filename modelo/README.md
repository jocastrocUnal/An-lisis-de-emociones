# Análisis de emociones con 6 lineas de código
[fuente](https://medium.com/qu4nt/an%C3%A1lisis-de-sentimientos-en-espa%C3%B1ol-con-seis-l%C3%ADneas-de-c%C3%B3digo-2d21cf82b7b4)

Sin más preámbulos, aquí va el código:

```python
from transformers import pipeline


classifier = pipeline('sentiment-analysis', 
                      model="nlptown/bert-base-multilingual-uncased-sentiment")

sentences = ["¡Me encantan los artículos de Medium, son lo máximo!", 
                "Odio los lunes, no sirven para nada.", 
                "El libro es medio bueno; me gustaron algunos personajes."]

results = classifier(sentences)
for result in results:
    print(f"polaridad: {result['label']}, score: {round(result['score'], 4)}")
```

El resultado es una clasificación de análisis de sentimientos para cada cadena de la lista sentences:

```
polaridad: 5 stars, score: 0.9102 
polaridad: 1 star, score: 0.9125 
polaridad: 3 stars, score: 0.7746
```

En este caso, la polaridad sigue un sistema de estrellas (como la de las reseñas de Amazon): una escala que va desde “no me gusta” (una estrella) a “me gusta” (cinco estrellas). El score indica qué tan seguro está el modelo de la clasificación realizada en cada caso.

Y eso es todo. Para ponerlo a funcionar debes instalar en tu sistema (con pip o conda) la librería transformers, así:

```python
$ pip install transformers
```

## La explicación

En el código de más arriba hemos utilizado una librería impresionante denominada 🤗 Transformers (sí, así mismo, con el emoji y todo) y que forma parte del proyecto de HuggingFace. Te recomiendo que te des un paseo por esa comunidad que está haciéndonos la vida mucho más fácil a quienes estamos interesados en la Inteligencia Artificial, y en particular a los que trabajamos con Procesamiento de Lenguaje Natural.

La gente de HuggingFace ha puesto en un único sitio un buen número de modelos de Deep Learning entrenados para tareas de NLP, además de una gran cantidad de datasets en varios idiomas. Y no contentos con eso han desarrollado un API que te permite, como en el ejemplo de arriba, utilizar tecnología de punta con unas pocas líneas de código.

El código funciona para hacer análisis de sentimientos (sentiment analysis) en español — utiliza un modelo llamado Bert-base entrenado específicamente para el análisis de sentimientos — , pero es multiidioma, así que también lo puedes utilizar para el inglés, francés, holandés, italiano y alemán.
