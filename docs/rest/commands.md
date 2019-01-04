# Módulo: rest-commands

En este módulo, ubicado en rest/management/commands, se encuentran los comandos personalizados de Django para gestionar los datos del servidor REST. 
Estos comandos pueden ser programados para gestionar automáticamente el servidor.

## batchClassification.py

**Autores**

* Antonio Cipagauta, 05-38040 | Douglas Torres, 11-11027

**Descripción**

Comando que llama a la función del módulo classifier que busca todas las medicinas conocidas (guardadas en la variable *medicines_list*) en Twitter, clasifica los tweets y los guarda en la BD.

#### Uso:
  
    python manage.py batchClassification

## eraseTweets.py

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

**Descripción**

Comando que elimina todos los tweets de la BD.

#### Uso:
  
    python manage.py eraseTweets

## expireTweets.py

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

**Descripción**

Comando que elimina los tweets que han llegado a su fecha de vencimiento. La variable del módulo de configuración "TWEET_EXPIRATION" define cuantos días tarda un tweet en expirar.

#### Uso:
  
    python manage.py expireTweets

## loadmeds.py

**Autores**

* Antonio Cipagauta, 05-38040 | Douglas Torres, 11-11027

**Descripción**

Comando que carga la lista de medicinas y componentes activos a la BD. Recibe como argumento la dirección del archivo donde se encuentran las medicinas. Para **Diciembre 2018** es: data/baseDatos-completa.csv.

#### Uso:
  
    python manage.py loadmeds [archivo con lista de medicinas]
