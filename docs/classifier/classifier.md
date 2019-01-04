# Módulo: classifier

En este módulo se encuentran los programas de clasificación y entrenamiento de la máquina clasificadora de tweets. 
Esta máquina clasifica tweets en **oferta**, **demanda** y **ninguno**. Para usos del *BuscaMed Server*, solo guardamos los tweets clasificados como **oferta**.

## classifier.py

**Autores**

* Version 1.0: Antonio Cipagauta, 05-38040 | Douglas Torres, 11-11027
* Version 2.0: Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770
* Version 2.1: Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

**Descripción**

Archivo donde se encuentran tres versiones del clasificador, separadas por comentarios (esto para mantener la retro-compatibilidad y para adoptar, sin cambios, varias cosas de la primera versión en las otras). Este clasificador hace uso de Tweepy para acceder al API de Twitter y realizar las búsquedas de medicinas, para luego clasificar los tweets y guardarlos en la BD.

### Versión 1.0

#### Clase Tweet:

Utilizada para facilitar la manipulación de los datos obtenidos del API de Twitter
    
    class Tweet:   
        def __init__(self, url, text, medicines):
            self.url = url
            self.text = text
            self.medicines = medicines

        def set_cluster(self, cluster):

        def get_id(self):

#### tweepy_auth:

Devuelve un objeto api de Tweepy que permite realizar las búsquedas a Twitter. 
Recibe un diccionario con el siguiente formato:
    
    keys = [{"consumer_key": "xxxx", "consumer_secret": "xxxx",
             "access_token": "xxxx", "access_secret": "xxxx"}]

    def tweepy_auth(keys) -> tweepy.api

#### clean:

Devuelve un objeto Tweet a partir de un tweet crudo obtenido por el API de Twitter.

    def clean(tweet): -> Tweet

#### classify:

Devuelve un objeto Tweet ya clasificado en **oferta** o **demanda**, a partir de un tweet crudo obtenido por el API de Twitter.

    def classify(raw_tweet): -> Tweet

#### batchClassify:

Busca todas las medicinas conocidas (guardadas en la variable *medicines_list*) en Twitter, clasifica los tweets y los guarda en la BD.

    def batchClassify(): -> None

### Versión 2.0

#### listarTweets:

Busca una lista de medicinas dada en Twitter, clasifica los tweets y los guarda en la BD.

*Opcional:* recibe un id de un tweet para buscar solamente tweets más recientes.

    def listarTweets(medicine_list, from_id=None): -> None

### Versión 2.1

#### Clase ListarThread:

Utilizada para generar hilos que busquen listas de medicinas concurrentemente en Twitter con diferentes API keys.

**ListarThread.run()** es equivalente a *listarTweets()*.
    
    class ListarThread(threading.Thread):
        def __init__(self, keys, medicine_list, from_id):
            threading.Thread.__init__(self)
            self.keys = keys
            self.medicine_list = medicine_list
            self.from_id = from_id

        def run(self):

#### threadingTweets:

Función que recibe una lista de API keys y una lista de medicinas, divide la lista de medicinas entre todas las API keys y crea hilos de *ListarThread*. Cada hilo tiene una API key y una sublista de medicinas, de esta manera se distribuye la carga de búsqueda entre las API keys.

*Opcional:* recibe un id de un tweet para buscar solamente tweets más recientes.

    def threadingTweets(keys, medicine_list, from_id=None): -> None


## train.py

**Autores**

* Version 1.0: Antonio Cipagauta, 05-38040 | Douglas Torres, 11-11027

**Descripción**

Archivo que contiene el programa principal que se encarga de entrenar el modelo utilizado por el clasificador de tweets. 

Los datos de todas las posibles medicinas los obtiene de:
    
    ../data/baseDatos-completa.csv

Los datos clasificados para entrenar los obtiene de:

    ../data/tweetsClasificados-3000.csv
