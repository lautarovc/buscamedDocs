# Módulo: buscaMedServer

En este módulo se encuentra definida la configuración general del projecto de Django.

## settings.py

En este archivo se encuentran definidas las variables globales y las configuraciones generales del proyecto.

Vale la pena destacar las siguientes:

* **DEBUG:** Variable que permite hacer uso de la aplicación mientras de desarrolla.
* **ALLOWED_HOSTS:** Arreglo donde se definen las direcciones donde puede correr la aplicación.
* **INSTALLED_APPS:** Arreglo donde se definen las librerias y modulos de la aplicación.
* **DATABASES:** Configuración general de la base de datos asociada a la aplicación.
* **REST_FRAMEWORK:** Configuración del API Rest (paginación, autenticación de acceso)
* **LOGIN_REDIRECT_URL:** URL donde se redirige una vez iniciada sesión.
* **LOGOUT_REDIRECT_URL:** URL donde se redirige una vez cerrada sesión.
* **django_heroku.settings(locals()):** Función que configura automáticamente las configuaraciones en Heroku (Incluida la BD)
* **TWITTER_AUTH:** Variable donde se guardan las API keys de Twitter a utilizar. Lleva el siguiente formato:
>>[{"consumer_key": "xxxx", "consumer_secret": "xxxx", "access_token": "xxxx", "access_secret": "xxxx"}]

* **TWEET_UPDATE:** Variable que define los minutos que deben pasar a partir de la búsqueda de un medicamento para volver a buscarlo en Twitter. Es decir, si pasan menos minutos para volver a buscar un mismo medicamento, muestra los tweets de la BD. Si pasan más minutos, vuelve a buscarlo en Twitter.
* **TWEET_EXPIRATION:** Variable que define los días que deben pasar para que un Tweet sea considerado "Expirado" y al llamar al comando *expireTweets* se elimine.
* **STORE_EXPIRATION** Variable que define los días que deben pasar para que el inventario de una tienda adscrita sea considerado "Expirado" y al llamar al comando *expireStoreInventory* se elimine.

## urls.py

En este archivo están definidas todas las urls de la aplicación. Para esto, importa todos los archivos *urls.py* de cada módulo.

Para esto define una variable *urlpatterns* con la siguiente estructura:

    urlpatterns = [
    	path('', HomeView.as_view(), name='home'), # URL DEL HOMEPAGE
    	url(r'^rest/', include('rest.urls')), # URLS DEL API REST
    	url(r'^stores/', include('stores.urls')), # URLS DE LA APP DE TIENDAS
    	url(r'admin/', admin.site.urls), # URLS ADMINISTRATIVAS
	]