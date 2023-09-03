# api-usuario
Proyecto para módulo 3 diplomado Full-Stack
Api de usuario realizado en Python con Flask
Los pasos para ejecutar el proyecto son los siguientes:

1.- Crear la Base de Datos diplomado en Postgres ejecutando el siguiente script:
CREATE DATABASE diplomado
    WITH
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'Spanish_Bolivia.1252'
    LC_CTYPE = 'Spanish_Bolivia.1252'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1
    IS_TEMPLATE = False;

2.- Crear las siguientes tablas dentro de la Base de datos diplomado:
CREATE TABLE public.usuario
(
    id_usuario character(36) COLLATE pg_catalog."default" NOT NULL,
    nombre character varying(50) COLLATE pg_catalog."default",
    primer_apellido character varying(50) COLLATE pg_catalog."default",
    segundo_apellido character varying(50) COLLATE pg_catalog."default",
    cedula_identidad character varying(15) COLLATE pg_catalog."default",
    fecha_nacimiento date,
    CONSTRAINT usuario_pkey PRIMARY KEY (id_usuario)
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.usuario
    OWNER to postgres;
    
CREATE TABLE public.datos_api
(
    id bigint NOT NULL,
    nombre_api character varying(30) COLLATE pg_catalog."default",
    version character varying(10) COLLATE pg_catalog."default",
    "desarrolladoPor" character varying(70) COLLATE pg_catalog."default",
    email character varying(30) COLLATE pg_catalog."default",
    estado character varying(8) COLLATE pg_catalog."default",
    CONSTRAINT datos_api_pkey PRIMARY KEY (id)
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.datos_api
    OWNER to postgres;

3. Si no se encuentra instalado virtualenv, procedemos a instalarlo:
pip install virtualenv
4. Creamos el entorno virtual:
python -m virtualenv venv
5. activar el entorno virtual:
.\venv\Scripts\activate
6. Si aparece el error activate.ps1 porque la ejecución de scripts está deshabilitada en este sistema:
ir al menú de windows y buscar powerShell.
Una vez en el powerShell escribir el siguiente comando:
Get-ExecutionPolicy -list
Set-ExecutionPolicy RemoteSigned -Force
7.- Abrir el ejecutar y escribir gpedit.msc, luego ir a Plantillas administrativas->Componentes de windows y buscar windows powerShell, una vez seleccionemos dicha opción nos vamos a la parte derecha y buscamos la opción "Activar la ejecución de scripts" y la abrimos, una vez dentro buscamos la opción Habilitada y en opciones buscamos la opción "Permitir solo scripts firmados", aplicamos los cambios y lo cerramos.
8. Volvemos al visual studio code y ejecutamos el entorno virtual.
.\venv\Scripts\activate
9. listamos todos los paquetes que tenemos instalados:
pip list
10. Istalamos flask, flask-cors, psycopg2, python-decouple, python-dotenv:
pip install flask flask-cors psycopg2 python-decouple python-dotenv
11. Hacer correr el programa:
python .\src\app.py

Para ejecutar las apis se sugiere utilizar postman, las direcciones son las siguientes:
1.- Para crear un usuario POST ‘/usuarios’
URL: localhost:5000/api/usuarios/usuarios
En postman vamos a la sección Body, dentro de ella seleccionamos la opción raw y el tipo JSON, luego agregamos lo siguiente:
{
  "nombre" : "Carlos ",
  "primerApellido" : "Pinto",
  "segundoApellido" : "Machicado",
  "cedulaIdentidad": "7045932",
  "fechaNacimiento" : "1994-08-21"
}

2.- Para listar a todos lo usuarios: GET ‘/usuarios’
URL: localhost:5000/api/usuarios/

3.- Para listar un usuario en especifico GET ‘/usuarios/:id_usuario’
URL: localhost:5000/api/usuarios/idUsuario

4.- Para actualizar los datos de un usuario: PUT ‘/usuarios/:id_usuario’
URL: localhost:5000/api/usuarios/usuarios/idUsuario
En postman vamos a la sección Body, dentro de ella seleccionamos la opción raw y el tipo JSON, luego agregamos lo siguiente:
{
  "nombre" : "Alain",
  "primerApellido" : "Ramos",
  "segundoApellido" : "Paredes",
  "cedulaIdentidad" : "7394201",
  "fechaNacimiento" : "2000-01-25"
}

5.- Para eliminar a un usuario: DELETE ‘usuarios/:id_usuario’
URL: localhost:5000/api/usuarios/usuarios/idUsuario

6.- Para mostrar el promedio de edades de los usuarios: GET ‘/usuarios/promedio-edad’
URL: localhost:5000/api/usuarios/promedio-edad/

7.- Para mostrar la version del api rest: GET ‘/estado’
URL: localhost:5000/api/usuarios/estado/
