# Módulo: rest-views

En este módulo se definen los controladores de las vistas de acceso al módulo REST utilizando el módulo *viewsets* del Django Rest Framework.

**Autores**

* Version 1.0: Antonio Cipagauta, 05-38040 | Douglas Torres, 11-11027
* Version 2.0: Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

## Funciones Auxiliares REST Tweets

#### searchDataBase:

**Versión 1.0**
Función que verifica que la medicina buscada por el usuario se encuentra en la base de datos y busca las medicinas equivalentes. Recibe el nombre de la medicina y devuelve componente activo, lista de equivalentes y un booleano que representa la existencia de un error.
    
    def searchDataBase(medName) -> (Activo, QuerySet<Medicina>, bool)

#### retrieveTweets:

**Versión 1.0**
Función que busca por cada Medicina en listaMedicinas los tweets asociados en la BD.

**Versión 2.0**
Filtra por tweets no expirados y ordena por fecha en orden decreciente. Devuelve la lista de Tweets encontrados.
    
    def retrieveTweets(listaMedicinas) -> QuerySet<Tweet>

#### buscaTweets:

**Versión 1.0**
Función que busca los tweets asociados a una medicina y todos sus equivalentes en la BD. Utiliza la función [searchDataBase](#searchdatabase) para encontrar los equivalentes a la medicina ingresada. Utiliza la función [retrieveTweets](#retrievetweets) para buscar los Tweets de la lista de medicinas obtenida por searchDataBase. Recibe el nombre de una medicina y devuelve la lista de Tweets.

**Versión 2.0**
Función reemplazada por [buscaTwitter](#buscatwitter), que se basa en esta para buscar en la BD.

    def buscaTweets(medName) -> QuerySet<Tweet>

#### buscaTwitter:

**Versión 2.0**<br>
Función que busca los Tweets asociados a una medicina y todos sus equivalentes en la BD.<br>
Si consigue Tweets en la BD, revisa si el Tweet más reciente fue buscado hace menos tiempo que los minutos definidos en la variable del módulo de configuración ["TWEET_UPDATE"](/buscaMedServer/buscaMedServer/#settingspy).<br>
Si fue buscado hace menos tiempo que dichos minutos, devuelve el query de la BD. En caso contrario, utiliza la función [threadingTweets](/classifier/classifier/#threadingtweets) del módulo *classifier* para buscar y clasificar Tweets a partir del id mas reciente de los Tweets en la BD.<br>
Si no consigue Tweets en la BD, realiza la búsqueda con la función [threadingTweets](/classifier/classifier/#threadingtweets) mencionada previamente.<br>
Recibe el nombre de una medicina, y devuelve una lista de Tweets y un booleano que define si se consiguió la medicina.

    def buscaTwitter(medName) -> (QuerySet<Tweet>, bool)


## Funciones Auxiliares REST Stores

#### getComponent:

**Versión 2.0**<br>
Función que busca el componente activo de un medicamento dado. Recibe el nombre de la medicina y devuelve una lista con un objeto Activo.

    def getComponent(medName) -> QuerySet<Activo>

#### retrieveInventory:

**Versión 2.0**<br>
Función que busca el componente activo de un medicamento en los inventarios de las farmacias asociadas. Para conseguir el componente activo, utiliza la función [getComponent](#getcomponent). Recibe el nombre de una medicina y devuelve una lista de los productos por tienda.

    def retrieveInventory(medName) -> QuerySet<ProductosPorTienda>

## Controladores de las Vistas

#### Clase TweetViewSet:

**Versión 2.0**<br>
Clase que hereda de viewsets.ReadOnlyModelViewSet del módulo *viewsets* del Django Rest Framework. Define la tabla de la BD que mostrará y el serializador que convertira las filas de la tabla en JSON.<br>
La función *list()* define la respuesta JSON a mostrar. Utiliza la función buscaTwitter y el serializador [TweetSerializer](/rest/serializers/#clase-tweetserializer).

    class TweetViewSet(viewsets.ReadOnlyModelViewSet):
        queryset = Tweet.objects.all()
        serializer_class = TweetSerializer

        def list(self, request, pk=None):
            ...
            return Response(queryset)

#### Clase StoresViewSet:

**Versión 2.0**<br>
Clase que hereda de viewsets.ReadOnlyModelViewSet del módulo *viewsets* del Django Rest Framework. Define la tabla de la BD que mostrará y el serializador que convertira las filas de la tabla en JSON.<br>
La función *list()* define la respuesta JSON a mostrar. Utiliza la función [retrieveInventory](#retrieveinventory) y el serializador [InventorySerializer](/stores/serializers/#clase-inventoryserializer).

    class StoresViewSet(viewsets.ReadOnlyModelViewSet):
        queryset = store.ProductosPorTienda.objects.all()
        serializer_class = storeSerializers.InventorySerializer

        def list(self, request, pk=None):
            ...
            return Response(queryset)

#### Clase WebViewSet:

**Versión 2.0**<br>
Clase que hereda de viewsets.ViewSet del módulo *viewsets* del Django Rest Framework. No necesita definir una tabla en la BD ni un seralizador, porque las herramientas del módulo [WebCrawler](/webcrawler/webcrawler/) ya devuelven un objeto compatible con JSON.<br>
La función *list()* realiza las búsquedas, las concatena y las devuelve en la respuesta.

    class WebViewSet(viewsets.ViewSet):
        def list(self, request):
            ...
            return Response(queryset)