# Módulo: stores-urls

En este módulo se encuentran definidas las URL para el acceso al módulo de la aplicación web.

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

#### urlpatterns:

Lista donde se definen los URL. *Nótese* que se utiliza la vista de authViews para hacer el cierre de sesión, que redirige a index.html.
    
    urlpatterns = [
        path('readFile', views.StoresView.as_view(), name='readFile'),
        path('login/', views.UserLoginView.as_view(), name='login'),
        path('logout/', authViews.LogoutView.as_view(template_name='index.html'), name='logout',),
    ]   
