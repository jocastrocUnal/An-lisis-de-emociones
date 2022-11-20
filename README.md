# Análisis de emociones

Desde la Api de YouTube, se extraen los comentarios de un video y se realiza un análisis de emociones. En este cuaderno se da una función que permite realizar el scraping de los comentarios desde la Api de YouTube. Tambien se implementa una limpieza de los comentarios haciendo uso de Hunspell. Al final con una red nuronal preentrenada se hace la clasificación de los comentarios.

## Prerequisitos

Las siguientes librerías son clave para la ejecución del código.

```python
!sudo apt-get update
!sudo apt-get install python-dev 
!sudo apt-get install libhunspell-dev

!pip install transformers
!pip install transformers[sentencepiece]

!pip install wordcloud
```
