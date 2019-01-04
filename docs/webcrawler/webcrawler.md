# Módulo: webcrawler

En este módulo se encuentran los webcrawlers que buscan la información de inventario directamente en las páginas web de diferentes farmacias. Utilizan el módulo *requests* para hacer las peticiones a las páginas y *BeautifulSoup* para analizar las respuestas HTML en Python.


## webCrawlerFarmarket.py

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

**Descripción**

Archivo donde se encuentran las funciones que permiten las búsquedas en la página de **Farmarket**.<br>
Contiene un *Main* para realizar pruebas directamente.

#### webCrawler:

Función que hace una petición POST (con timeout=30seg) a la página de *Farmarket* con la variable 'txtProducto' asignada al valor de la medicina. Luego, la respuesta es analizada por *Beautiful Soup* y la información de los productos es recolectada por la función *collectInfo*. 
    
    def webCrawler(medicine): -> List<ProductosPorTienda>

#### collectInfo:

Recibe una lista de los tds (table data) del HTML, obtenida por *BeautifulSoup*, y de forma personalizada a la estructura de la página de *Farmarket*, recolecta la información de los productos por tienda en una lista.

    def collectInfo(tds): -> List<ProductosPorTienda>



## webCrawlerFullFarmacia.py

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

**Descripción**

Archivo donde se encuentran las funciones que permiten las búsquedas en la página de **FullFarmacia**.<br>
Contiene un *Main* para realizar pruebas directamente.

#### webCrawler:

Función que hace una petición GET (con timeout=30seg) a la página de *FullFarmacia* con la variable 'searchBox' asignada al valor de la medicina. Luego, la respuesta es analizada por *Beautiful Soup* y la información de los productos es recolectada por la función *collectInfo*. 
    
    def webCrawler(medicine): -> List<ProductosPorTienda>

#### collectInfo:

Recibe una lista de los tds (table data) dentro de 'productContainer' del HTML, obtenida por *BeautifulSoup*, y de forma personalizada a la estructura de la página de *FullFarmacia*, recolecta la información de los productos por tienda en una lista.

    def collectInfo(tds): -> List<ProductosPorTienda>



## webCrawlerFundafarmacia.py

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

**Descripción**

Archivo donde se encuentran las funciones que permiten las búsquedas en la página de **Fundafarmacia**.<br>
Contiene un *Main* para realizar pruebas directamente.

#### webCrawler:

Función que hace una petición POST (con timeout=30seg) a la página de *Fundafarmacia* con la variable 'producto' asignada al valor de la medicina. Luego, la respuesta es analizada por *Beautiful Soup* y la información de los productos es recolectada por la función *collectInfo*. 
    
    def webCrawler(medicine): -> List<ProductosPorTienda>

#### collectInfo:

Recibe una lista de los tds (table data) del HTML, obtenida por *BeautifulSoup*, y de forma personalizada a la estructura de la página de *Fundafarmacia*, recolecta la información de los productos por tienda en una lista.

    def collectInfo(tds): -> List<ProductosPorTienda>
