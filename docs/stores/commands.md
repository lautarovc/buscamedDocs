# Módulo: stores-commands

En este módulo, ubicado en stores/management/commands, se encuentran los comandos personalizados de Django para gestionar los datos de los inventarios de las farmacias adscritas. 
Estos comandos pueden ser programados para gestionar automáticamente el servidor.

## expireStoreInventory.py

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

**Descripción**

Comando que elimina los productos por tienda que han llegado a su fecha de vencimiento. La variable del módulo de configuración "STORE_EXPIRATION" define cuantos días tarda el inventario de una tienda en expirar.

#### Uso:
  
    python manage.py expireStoreInventory
