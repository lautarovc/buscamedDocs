# Bienvenido

Esta es la documentación del servidor de [Buscamed Venezuela](http://buscamed.org.ve).

Este programa está configurado para funcionar en Heroku, pero puede ser utilizado localmente
con las siguientes instrucciones.

## Autores:
* Lautaro Villalón, 12-10427
* Yarima Luciani, 13-10770
* Yezabel Rincón, 10-11005

### Instalación

* #### Configuracion de la BD:

	+ `$`sudo apt-get update

	+ `$`sudo apt-get install python3-pip python3-dev libpq-dev postgresql postgresql-contrib

	+ `$`sudo -u postgres psql

	+ `postgres=#`CREATE DATABASE buscamedserver;

	+ `postgres=#`CREATE USER buscameduser WITH PASSWORD [contraseña];

	+ `postgres=#`ALTER ROLE buscameduser SET client_encoding TO 'utf8';

	+ `postgres=#`ALTER ROLE buscameduser SET default_transaction_isolation TO 'read committed';

	+ `postgres=#`ALTER ROLE buscameduser SET timezone TO 'UTC';

	+ `postgres=#`GRANT ALL PRIVILEGES ON DATABASE buscamedserver TO buscameduser;

	+ `postgres=#`\q

	+ `$`sudo ufw allow 8000


* #### Primera Corrida:
**Nota: Es recomendable usar un virtual environment**

	+ `$`pip install -r requirements.txt

	+ `$`python manage.py makemigrations 

	+ `$`python manage.py migrate 

	+ `$`python manage.py createsuperuser 
	**(user: admin, email: admin@admin.com)**

	+ `$`python manage.py loadmeds data/baseDatos-completa.csv

	+ `$`python manage.py runserver 0.0.0.0:8000

	**Escribir en un browser 127.0.0.1:8000**

### Funcionamiento general

* Incluye un API rest con varios accesos para obtener datos de medicinas en Venezuela:
	+ /rest/tweets?med=[medicina]
	+ /rest/web/?med=[medicina]
	+ /rest/stores/?med=[medicina]

* Incluye un homepage que hace uso del API rest para mostrar los datos
* Inlcuye una aplicación de acceso a usuarios de farmacias para que puedan enviar sus inventarios en formato .CSV
	+ /stores/login
	+ /stores/readFile
