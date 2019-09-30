# TutorialAWS

## Pagina Estatica S3

### Crear Bucket
1. Buscar S3 en los servicios de AWS
2. Crear un Bucket
3. Llenar los datos en la seccion "Name and Section"
4. en la pestaña de "Set permission" desmarcar la casilla "Block all public access"
5. Dar click en Create Bucket

### Agregar archivos y permisos
Una vez adentro del bucket
1. Dar click en el botón de "Upload"
2. Dar click en el botón de "Add files"
3. Buscar los archivos que se van a subir
4. Cargar los archivos
5. Ir a la seccion de Properties y seleccionar "Static website hosting"
6. Seleccionar la opción "Use thus bucket to host a website"
7. Ir a la seccioón "Permissions" y en Bucket policy copiar el siguiente codigo

````
{
  "Version":"2012-10-17",
  "Statement":[{
	"Sid":"PublicReadGetObject",
        "Effect":"Allow",
	  "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::example-bucket/*"
      ]
    }
  ]
}
````
8. Entrar a la URL que genero el Bucket

## Pagina Dinamica Base de datos y EC2

### Establecer la base de datos
 
1. Buscar el RDS en el buscador de servicios de AWS
2. Carle click a "crete database"
3. Es coger el tipo de base de datos que se quiera crear
4. Llenar los datos siguientes, no olvidar llenar los siguientes datos
  - Nombre de la base de datos
  - Id de la base de datos
  - Nombre del usuario
  - Contrase;a del usuario
  - Configuracion de la VPC (publica)
  
5. Crear base de datos
6. Configurar los grupos de seguridad asegurandose que el source sea 0.0.0.0/0
 
### Crear la maquina en EC2 y conectarse a la base de datos

1. Buscar EC2 en el buscador de servicios de AWS
2. Dar click en "Launch Instance"
3. Escoger la maquina de ubuntu 18.04
4. Escoger la llave que se quiera para conectase por SSH y lanzar la instancia
5. COnfigurar los security groups. Asegurarse que se tengan las siguientes reglas
  - HTTP:80 0.0.0.0/0
  - SSH: 22 0.0.0.0/0
  - PostgresQL:5432 0.0.0.0/0
6. Crear una pagina dinamica. Si se crea en java con Spring configurar el archivo "aplication.properties" de la siguiente manera
````
mvnspring.main.banner-mode = off

#Puerto donde se lanzara la aplicacion
server.port = 80

#Conexion a la base de datos.
spring.datasource.driver-class-name = org.postgresql.Driver
spring.datasource.url = jdbc:postgresql://database-webpage.cjbvphxx6lf6.us-east-1.rds.amazonaws.com:5432/postgresWebPage
spring.datasource.username = postgresWebPage
spring.datasource.password = password80
````
7. Subir los archivo a la maquina virtual de EC2
8. Descargar e instalar todo lo necesario para compilar y correr la pagina dinamica
9. Correr la pagina e intentar abrirla desde una navegador externo
