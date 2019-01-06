# Módulo: stores-readFile.js

En este módulo se encuentran las funciones de JavaScript y jQuery que permiten leer un archivo CSV y enviarlo por POST al controlador del módulo [stores](../../../stores/views/#clase-storesview) que permite agregar un inventario a la BD.

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

#### checkData:

Función que recibe datos de un archivo CSV y revisa que tenga las columnas: *activo | medicina | presentacion | disponibilidad*.

    function checkData(data) -> bool

#### readCSV:

Función que obtiene el valor del archivo escrito en *#fileName*, revisa que sea CSV, lee el archivo con el módulo *FileReader* de JavaScript, convierte a objeto JSON con el módulo *csv.toObjects* de jQuery.CSV, revisa las columnas con [checkData](#checkdata) y envía el objeto en forma de *String* al controlador del módulo [stores](../../../stores/views/#clase-storesview) a través de una petición POST.

    function readCSV() -> HTML: asigna variable "#csv" y envia formulario "#Login" 