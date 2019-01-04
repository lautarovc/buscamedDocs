# Módulo: stores-serializers

En este módulo se encuentran definidos los serializadores para convertir los objetos de la BD de las farmacias adscritas en objetos JSON. Utiliza el módulo *serializers* del Django Rest Framework.

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

#### Clase StoreSerializer:

Define la estructura en JSON de una tienda (usuario de Django).<br>
**Nota:** La dirección de cada tienda esta guardada en la variable *last_name* del usuario.

**Ejemplo:** {'nombre': User.first_name, 'direccion': User.last_name}.
    
    class StoreSerializer(serializers.ModelSerializer):
        nombre = serializers.SerializerMethodField()
        direccion = serializers.SerializerMethodField()
        class Meta:
            model = User
            fields = ('nombre','direccion')
            read_only_fields = ('nombre','direccion')
        def get_nombre(self, obj):
            return obj.first_name
        def get_direccion(self, obj):
            return obj.last_name


#### Clase ActivoSerializer:

Define la estructura en JSON de un componente activo.

**Ejemplo:** {'componente': Activo.componente}.
    
    class ActivoSerializer(serializers.ModelSerializer):
        class Meta:
            model = Activo
            fields = ('componente',)
            read_only_fields = ('componente',)


#### Clase MedicinaSerializer:

Define la estructura en JSON de una medicina.

**Ejemplo:** {'nombre': Medicina.nombre, 'activo': {'componente': Activo.componente}}.<br>
*Nótese* que Medicina.activo se serializa con el serializador [ActivoSerializer](#clase-activoserializer).
    
    class MedicinaSerializer(serializers.ModelSerializer):
        activo = ActivoSerializer()
        class Meta:
            model = Medicina
            fields = ('nombre', 'activo')
            read_only_fields = ('nombre', 'activo')


#### Clase PresentacionSerializer:

Define la estructura en JSON de una presentación de una medicina.

**Ejemplo:** {'presentacion': Presentacion.presentacion, 'medicina': {'nombre': Medicina.nombre, 'activo': {'componente': Activo.componente}}}.<br>
*Nótese* que Presentacion.medicina se serializa con el serializador [MedicinaSerializer](#clase-medicinaserializer).
    
    class PresentacionSerializer(serializers.ModelSerializer):
        medicina = MedicinaSerializer()
        class Meta:
            model = Presentacion
            fields = ('presentacion', 'medicina')
            read_only_fields = ('presentacion', 'medicina')


#### Clase InventorySerializer:

Define la estructura en JSON de un producto por tienda.

**Ejemplo:**  {'producto': {'presentacion': Presentacion.presentacion, 'medicina': {'nombre': Medicina.nombre, 'activo': {'componente': Activo.componente}}}, 'tienda': {'nombre': User.first_name, 'direccion': User.last_name}, 'disponibilidad': ProductosPorTienda.disponibilidad, 'fechaDeIngreso': ProductosPorTienda.fechaDeIngreso}.<br><br>
*Nótese* que ProductosPorTienda.producto se serializa con el serializador [PresentacionSerializer](#clase-presentacionserializer) y ProductosPorTienda.tienda se serializa con el serializador [StoreSerializer](#clase-storeserializer).

    class InventorySerializer(serializers.ModelSerializer):
        producto = PresentacionSerializer()
        tienda = StoreSerializer()
        class Meta:
            model = ProductosPorTienda
            fields = ('producto', 'tienda', 'disponibilidad', 'fechaDeIngreso')
            read_only_fields = ('producto', 'tienda', 'disponibilidad', 'fechaDeIngreso')
