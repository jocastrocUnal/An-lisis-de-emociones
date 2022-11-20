# Hunspell – Corrector ortográfico
[fuente](https://recursospython.com/guias-y-manuales/hunspell-corrector-ortografico/)

Hunspell es un corrector ortográfico multiplataforma, utilizado por software de primera línea como Mozilla Firefox, Thunderbird, Google Chrome, LibreOffice, entre otros. Provee su funcionalidad a través de la librería libhunspell y accedemos desde Python vía el módulo PyHunspell, desarrollado por Benoît Latinier.

Descarga e instalación
Usuarios de Microsoft Windows pueden descargar instaladores para las versiones 2.7 y 3.5 vía windows.recursospython.com.

En distribuciones de Linux, puede utilizarse:

```python
pip install hunspell
```

O bien descargar el código de fuente desde PyPI o el proyecto en GitHub y ejecutar:

```python
python setup.py install
```

Ambos métodos requieren los paquetes python-dev y libhunspell-dev.

Diccionarios
Hunspell utiliza diccionarios para proporcionar la verificación ortográfica y análisis morfológico. Puedes obtener el diccionario para la lengua española (utilizado en los ejemplos) desde este enlace.

Los siguientes enlaces proveen diccionarios para el resto de las lenguas.

LibreOffice
Extensiones de LibreOffice
Mozilla Add-Ons
Ejemplos
Importar el módulo y cargar el diccionario español.

```python
import hunspell
dic = hunspell.HunSpell("es_ANY.dic", "es_ANY.aff")
```
```python
dic.spell("recursos")
```
```
True
```
```python
dic.spell("python")
```
```
False
```
«Python» es una palabra inglesa, lógicamente no se encuentra en el diccionario español. De todas formas, podemos agregarla.

```python
dic.add("python")
```
```
0
```
```python
dic.spell("python")
```
```
True
```

Como también eliminar palabras.

```python
dic.spell("hola")
```
```
True
```

```python
dic.remove("hola")
```
```
0
```


```python
dic.spell("hola")
```
```
False
```

Nótese que las funciones Hunspell.add y Hunspell.remove operan con el diccionario cargado en memoria. Los cambios no se ven reflejados en el archivo del sistema (en este caso, es_ANY.dic).

(Desafortunadamente, una instancia Hunspell no puede ser serializada vía pickle. Sin embargo, no sería mucho trabajo almacenar las palabras añadidas en un archivo de texto y cargarlo en la próxima ejecución, utilizando las funciones anteriores.)

Para obtener sugerencias de una palabra:

```python
dic.suggest("python")
```
```
['poncho']
```

```python
dic.suggest("cosinar")
```
```
['cocinar', 'copinar', 'narcosis', 'consignar', 'sincopar', 'narcotina']
```

```python
dic.suggest("varajar")
```
```
['barajar', 'va rajar', 'va-rajar', 'varar', 'rajar', 'vara']
```

```python
dic.suggest("inalar")
```
```
['inhalar', 'inflar', 'in alar', 'in-alar', 'instalar', 'inclinar', 'alminar', 'laminar']
```

Analizar morfológicamente y obtener el infinitivo de un verbo:

```python
dic.analyze("tomé")
```
```
[' st:tomar fl:R']
```

```python
dic.stem("tomé")
```
```
['tomar']
```

Por último, la función Hunspell.get_dic_encoding retorna la codificación de caracteres utilizada por el diccionario. Por ejemplo, en Python 2, el siguiente código solicita una palabra e imprime en pantalla todas las sugerencias. Si nuestra terminal utiliza una codificación diferente (por ejemplo, cp850 en Windows) debemos realizar las conversiones necesarias.

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import hunspell
import sys
dic = hunspell.HunSpell("es_ANY.dic", "es_ANY.aff")
while True:
    word = raw_input("> ").decode(sys.stdin.encoding)
    if word:
        for suggest in dic.suggest(word):
            print suggest.decode(dic.get_dic_encoding())
```
```
> tomé
tome
tomé
Tomé
timé
toné
toé
toma
temé
tomo
tosé
tocé
comé
domé
topé
tomó
```
