# Módulo: rest-models

En este módulo se encuentra definida la estructura de la base de datos en un modelo orientado a objetos utilizando el Django ORM original.

**Autores**

* Version 1.0: Antonio Cipagauta, 05-38040 | Douglas Torres, 11-11027
* Version 2.0: Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

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

Guarda la presentación y registro sanitario asociado a una medicina.

**Versión 2.0:** Tabla sin utilizar por ser innecesaria hasta los momentos. Guardar las presentaciones ocupa más espacio del permitido por las limitaciones gratuitas de Heroku. Definida igualmente para expansión futura.

    class Presentacion(models.Model):
        presentacion = models.TextField(verbose_name=('Presentacion'))
        registro = models.TextField(verbose_name=('Registro sanitario'))
        medicina = models.ForeignKey(Medicina, related_name='formato',null=True, on_delete=models.CASCADE)

#### Clase Tweet:

Guarda cada tweet con su URL y tipo de clasificación (Oferta/Demanda), asociado a una medicina.

**Versión 2.0:** Guarda fecha de búsqueda de cada tweet para optimizar las búsquedas y calcular la expiración. Define una función que permite obtener el id de cada tweet a partir de su URL.

    class Tweet(models.Model):
        link = models.TextField(verbose_name=('Link'),unique=True)
        clasificacion = models.TextField(verbose_name=('Clasificacion'))
        medicina = models.ForeignKey(Medicina, related_name='Medicina', null=True, on_delete=models.CASCADE)
        fecha = models.DateTimeField(auto_now_add=True, blank=True)

    def getId(self):
        tweetId = self.link.split("/")[-1]
        return int(tweetId)
