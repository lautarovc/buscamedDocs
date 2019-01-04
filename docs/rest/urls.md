# Módulo: rest-urls

En este módulo se encuentran definidas las URL para el acceso al módulo REST. Para esto se utiliza el módulo *routers* del Django Rest Framework.

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

#### router:

Variable donde se registran las vistas del módulo *rest-views*. Esta variable es un objeto *DefaultRouter* del Django Rest Framework.

    router = routers.DefaultRouter()
    router.register(r'tweets', views.TweetViewSet)
    router.register(r'stores', views.StoresViewSet)
    router.register(r'web', views.WebViewSet, base_name='web')

#### urlpatterns:

Lista donde se definen los URL. *Nótese* que al incluir la variable router.urls, se incluyen automáticamente todas las URL asociadas a las vistas guardadas en la variable router.
    
    urlpatterns = [
    url(r'^', include(router.urls)),
    url(r'^api-auth/', include('rest_framework.urls', namespace='rest_framework'))]
