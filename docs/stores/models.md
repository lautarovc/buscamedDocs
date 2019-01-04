# Módulo: stores-models

En este módulo se encuentra definida la estructura de la base de datos para los inventarios de farmacias adscritas en un modelo orientado a objetos utilizando el Django ORM original.

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

#### Clase Activo:

Guarda cada componente activo sin repeticiones.
    
    class Activo(models.Model):
        componente = models.TextField(verbose_name=('Componente activo'),unique=True)

#### Clase Medicina:

Guarda cada medicina asociada a un componente activo.
    
    class Medicina(models.Model):
        nombre = models.TextField(verbose_name=('Nombre de marca'))
        activo = models.ForeignKey(Activo, related_name='componente-activo+', null=True, on_delete=models.CASCADE)

#### Clase Presentacion:

Guarda la presentación asociada a una medicina.

    class Presentacion(models.Model):
        presentacion = models.TextField(verbose_name=('Presentacion'))
        medicina = models.ForeignKey(Medicina, related_name='formato',null=True, on_delete=models.CASCADE)

#### Clase ProductosPorTienda:

Asocia cada presentación de un producto con una tienda, su disponibilidad y su fecha de ingreso del dato. Esta tabla permite representar el inventario de cada tienda.

    class ProductosPorTienda(models.Model):
        producto = models.ForeignKey(Presentacion, related_name='med', null=True, on_delete=models.CASCADE)
        tienda = models.ForeignKey(User, related_name='tienda', null=True, on_delete=models.CASCADE)
        disponibilidad = models.IntegerField(verbose_name=('Disponibilidad'))
        fechaDeIngreso = models.DateTimeField(verbose_name=('Fecha de actualizacion'), auto_now_add=True, blank=True)
