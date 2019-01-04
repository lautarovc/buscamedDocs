# Módulo: stores-views

En este módulo se definen los controladores de las vistas para el módulo de la aplicación web utilizando el módulo *viewsets* del Django Rest Framework.

**Autores**

* Lautaro Villalón, 12-10427 | Yarima Luciani, 13-10770

## Controladores para vistas de farmacias adscritas

#### Clase LoginView:

Clase que hereda de LoginView del módulo *auth.views* de Django. Define el formulario de Django a utilizar para renderizar en el archivo html correspondiente (templates/registration/login.html).

En el archivo *stores/forms.py* se definen las características que se esperan renderizar del formulario de inicio de sesión de la siguiente manera:

    class LoginForm(AuthenticationForm):
        username = forms.CharField(widget=forms.TextInput(attrs={'class':'form-control', 'id':'inputEmail', 'placeholder':'Nombre de usuario'}))
        password = forms.CharField(widget=forms.PasswordInput(attrs={'class':'form-control', 'id':'inputPassword', 'placeholder':'Contraseña'}))

Esto se asigna en la clase del controlador de la siguiente manera:

    class UserLoginView(LoginView):
        form_class = LoginForm


#### Clase StoresView:

Clase que hereda de TemplateView del módulo *views.generic* de Django. Define las acciones a realizar cuando se accede a la página de lectura de archivo CSV del inventario para farmacias adscritas.

La función get se llama cuando se recibe una petición GET, en este caso, cuando no se envía un inventario.<br>
La función post se llama cuando se recibe una petición POST, en este caso, cuando se envía un inventario.

*Nótese* que cuando se accede por get, la variable success es renderizada con el valor -1, esto para que no se muestre ningun mensaje al usuario. Cuando se accede por post y el archivo es cargado con éxito, la variable success es renderizada con el valor 1, para mostrar un mensaje de carga exitosa. De la misma manera, si hay un error, se renderizará con valor 0 para mostrar un mensaje de error.


    class StoresView(TemplateView):
        def get(self, request):
            ...
            return render(request, 'readFile.html', {'success': -1})
        def post(self, request):
            ...
            return render(request, 'readFile.html', {'success': 1})

## Controlador de la vista pública de búsqueda

#### Clase HomeView:

Clase que hereda de TemplateView del módulo *views.generic* de Django. Define las acciones a realizar cuando se accede a la página de inicio y de búsqueda.<br>
Hasta ahora, todo el trabajo de la página de inicio se encuentra del lado del cliente, puede conseguir más información en [templates](/stores/templates/#indexhtml).


    class HomeView(TemplateView):
        def get(self, request):
            return render(request, 'index.html', {})
        def post(self, request):
            return render(request, 'index.html', {})
