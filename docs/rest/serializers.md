# Módulo: rest-serializers

En este módulo se encuentran definidos los serializadores para convertir los objetos de la BD en objetos JSON. Utiliza el módulo *serializers* del Django Rest Framework.

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

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

#### Clase TweetSerializer:

Define la estructura en JSON de un tweet.

**Ejemplo:**  {'id': Tweet.getId(), 'link': Tweet.link, 'medicina': {'nombre': Medicina.nombre, 'activo': {'componente': Activo.componente}}.<br>
*Nótese* que Tweet.medicina se serializa con el serializador [MedicinaSerializer](#clase-medicinaserializer).

    class TweetSerializer(serializers.ModelSerializer):
        medicina = MedicinaSerializer()
        id = serializers.SerializerMethodField()
        class Meta:
            model = Tweet
            fields = ('id','link', 'medicina')
            read_only_fields = ('id','link', 'medicina')
        def get_id(self, obj):
            return obj.getId()
