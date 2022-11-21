# Hunspell – Corrector ortográfico
Es un correctos ortográfico y un análizador morfológico, diseñado para idiomas con morfología y comsposición de palabras compleja. Creado por László Németh, como una alternativa para correctores anteriores como MySpell. Es el motor de revisión ortográfica predeterminado en Chrome y Firefox, Libre/OpenOffice,Thunderbird, productos de Adobe y macOS.\
Provee su funcionalidad a través de la librería libhunspell y accedemos desde Python vía el módulo PyHunspell, desarrollado por Benoît Latinier.
## Descarga e instalación
Se requieren los paquetes python-dev y libhunspell-dev.\
Usuarios de Microsoft Windows pueden descargar instaladores para las versiones 2.7 y 3.5. Y en el caso de distribuciones de Linux puede usarse

```python
pip install hunspell
```

O bien descargar el código de fuente desde PyPI o el proyecto en GitHub y ejecutar:

```python
python setup.py install
```
## Diccionarios 
Hunspell utiliza diccionarios para proporcionar la verificación ortográfica y análisis morfológico.Dichos diccionarios existen en la mayoría de lenguajes de uso en la actualidad.\
Un diccionario con formato Hunspell consiste de dos partes: 
* El archivo [lang].aff  especifica la sintaxis del afijo para el idioma.
* El archivo [lang].dic contiene una lista de palabras usando la sintaxis del archivo aff.
La carga de diccionarios se hace de la siguiente forma
```python
import hunspell
dic = hunspell.HunSpell("es_ANY.dic", "es_ANY.aff")
```
Para obtener el diccionario para la lengua española, haga click [aquí](https://recursospython.com/guias-y-manuales/hunspell-corrector-ortografico/#google_vignette). 
## ¿Cómo funciona? 
La corrección de palabras consiste en los siguientes pasos:
1. Analiza una frase extrayendo (tokenizing) las palabras que queremos chequear.
2. Analiza cada palabra desglosándola en su raíz (stemming) y afijo de conjugación.
3. Busca en el diccionario si la combinación palabra+afijo es válida para el idioma.
4. Para palabras incorrectas, sugiera correcciones buscando palabras similares (correctas) en el diccionario.
#### Tokenizing - Tokenizando
La tokenización consiste esencialmente en dividir una frase, oración, párrafo o un documento de texto en unidades más pequeñas, como palabras o subpalanras. Cada una de estas unidades más pequeñas se denomina tokens. Para este caso, Hunspell divide las frases en palabras y con estas procede a realizar el desglosamiento.

#### Stemming
Se divide la palabra en la raiz y en un afijo de conjugación. 
```python
dic.stem("lucecita")
```
[b'luz']

```python
dic.stem("enlazado")
```
[b'enlazar']

```python
dic.stem("tomé")
```
['tomar']
#### Análisis 
Función parecida a la anterior, sin embargo, en la salida se agrega el tipo de afijo. 
```python
dic.analyze("enlazado")
```
[b' st:enlazar fl:D']
```python
dic.analyze("lucecita")
```
[b' st:luz fl:U']

```python
dic.analyze("tomé")
```
[b' st:tomar fl:R']


#### Buscar,agregar y eliminar al diccionario
```python
dic.spell("recursos")
```
True
```python
dic.spell("python")
```
False

«Python» es una palabra inglesa por lo que no se encuentra en el diccionario español. De todas formas, se puede agregar.

```python
dic.add("python")
```
0
```python
dic.spell("python")
```
True

También se puede elimir palabras.
```python
dic.spell("hola")
```
True
```python
dic.remove("hola")
```
0
```python
dic.spell("hola")
```
False

#### Sugerencias a una palabra
Para obtener sugerencias de una palabra:
```python
dic.suggest("python")
```
['poncho']
```python
dic.suggest("cosinar")
```
['cocinar', 'copinar', 'narcosis', 'consignar', 'sincopar', 'narcotina']
## Referencias y fuentes
[Fuente 1](https://recursospython.com/guias-y-manuales/hunspell-corrector-ortografico/)\
[Fuente 2](https://cran.r-project.org/web/packages/hunspell/vignettes/intro.html#Installing_Dictionaries_in_RStudio)\
[Fuente 3](https://zverok.space/blog/2021-01-05-spellchecker-1.html)\
[Fuente 4](
