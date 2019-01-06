# Módulo: stores-homeSearch.js

En este módulo se encuentran las funciones de JavaScript y jQuery que permiten hacer una búsqueda dinámica en la página de inicio, llamando al servidor [REST](../../../rest/views/).

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

#### toggleTweets:

Minimiza o restaura la caja donde se muestran los tweets conseguidos.

    function toggleTweets() -> HTML: esconde un div

#### toggleWeb:

Minimiza o restaura la caja donde se muestran los productos conseguidos en farmacias.

    function toggleWeb() -> HTML: esconde un div

#### startSearch:

Hace la búsqueda a partir del valor escrito en *#searchBox* y llama a las funciones que, con Ajax, buscan y muestran los resultados.

    function startSearch() -> HTML: muestra div de resultados y llama funciones asincronas de busqueda

#### ajaxBuscamedTweets:

Función que recibe el nombre de una medicina y utiliza el módulo *ajax* de jQuery para hacer un llamado al [controlador de búsqueda en Twitter](../../../rest/views/#clase-tweetviewset) del servidor REST. Con el resultado, llama a la función [ajaxTwitter](#ajaxtwitter) para incrustar el tweet con el formato de Twittter.

    function ajaxBuscamedTweets(med) -> None

#### ajaxTwitter:

Función que recibe el url de un tweet, y utiliza el módulo *ajax* de jQuery para hacer un llamado al servidor REST de *publish.twitter.com* y obtener el código html para incrustar el tweet en la caja de tweets.

    function ajaxTwitter(tweetUrl) -> HTML: inserta resultado en div de tweets

#### ajaxBuscamedWeb:

Función que recibe el nombre de una medicina y utiliza el módulo *ajax* de jQuery para hacer un llamado al [controlador de búsqueda en web](../../../rest/views/#clase-webviewset) del servidor REST. Con el resultado, llama a la función [htmlForWeb](#htmlforweb) para obtener el formato en HTML predeterminado e incrustar el resultado.

    function ajaxBuscamedWeb(med) -> HTML: inserta resultado en div de farmacias

#### htmlForWeb:

Función que recibe el objeto obtenido por [ajaxBuscamedWeb](#ajaxbuscamedweb), y renderiza el objeto en un formato HTML predeterminado que puede ser incrustado en la página.

    function htmlForWeb(store) -> String: formato HTML

#### ajaxBuscamedStores:

Función que recibe el nombre de una medicina y utiliza el módulo *ajax* de jQuery para hacer un llamado al [controlador de búsqueda en farmacias adscritas](../../../rest/views/#clase-storesviewset) del servidor REST. Con el resultado, llama a la función [htmlForStores](#htmlforstores) para obtener el formato en HTML predeterminado e incrustar el resultado.

    function ajaxBuscamedStores(med) -> HTML: inserta resultado en div de farmacias

#### htmlForStores:

Función que recibe el objeto obtenido por [ajaxBuscamedStores](#ajaxbuscamedstores), y renderiza el objeto en un formato HTML predeterminado que puede ser incrustado en la página.

    function htmlForStores(store) -> String: formato HTML

