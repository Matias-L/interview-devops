<img src="https://i.ibb.co/VM5MzBT/craftech-logo3.png=150x" width="250" height="250">

#### Prueba 2 - Despliegue de una aplicación Django y React.js

El proyecto hace uso de dos dockerfiles, uno por cada componente (backend y front end). 
Para el caso del front end el mismo dockerfile se encarga de ejecutar los comandos necesarios para la compilación e inicialización del proyecto.
Este proyecto solo se ha probado en un ambiente de desarrollo localmente. Por esa razón, y por simplicidad, se realizó la orquestación mediante docker-compose.
Para el despliegue es necesario:
 * Tener instalados docker y docker compose. 
 * Clonar el repositorio
 * Estando en el directorio raiz del repositorio, mediante una consola ejecutar "docker-compose up --build"
 * Luego de haberlo ejecutado por primera vez, se puede levantar nuevamente el entorno mediante "docker-compose up" y frenar con "docker-compose down".  

Mientras las aplicaciones se estan ejecutando, podemos acceder al servicio backend en 0.0.0.0:8000 y al dashboard frontend desde localhost:3000


##### DESPLEGAR EN DIGITAL OCEAN

Podemos desplegar la aplicación en un droplet de DigitalOcean siguiendo los pasos a continuación. Se asume que tiene una cuenta activa.
1. Crear un droplet:
*  Elegir como distribución a Ubuntu (LTS) x64.
* La aplicación no consume muchos recursos, por lo que se puede elegir el plan básico de CPU compartida, Intel regular y 1 CPU.
* Configure la opción de autenticación. En este caso se utilizó autenticación por contraseña. IMPORTANTE: Si opta por autenticarse mediante contraseña, tome nota de la misma ya que no recibiremos los detalles de autenticación por ningún medio.
*  No es necesaria ninguna otra configuración. Queda a preferencia del usuario cambiar alguna opción, como ser etiquetas o ubicación del datacenter.
* Crear el droplet presionando "Create Droplet" y esperar a que se complete la barra de progreso. Una vez finalizado, obtendremos la IP pública de nuestro droplet.
2. Configuraciones iniciales del servidor: Debemos acceder por ssh a nuestro droplet mediante **ssh root@"ipPublicaDroplet"**. Utilizamos la contraseña generada en el paso 1.
3. Creamos un nuevo usuario. De esta forma, en el futuro ingresamos con este usuario en vez de root. Para ello ejecutamos el comando **adduser "usuario"**. Elegir una contraseña de usuario y completar los campos opcionales que se nos solicitan si así lo desea.
4. Dar privilegios administrativos al usuario creado. Para ello ejecutamos el comando **usermod -aG "sudo usuario"**. Esto coloca a nuestro usuario en la lista de *sudoers*
5. Corroborar que podemos ejecutar *sudo* con el nuevo usuario. Para ello, abrimos una sesión nueva de SSH e ingresamos con el nuevo usuario. Luego, ejecutar algun comando simple con *sudo* y corroborar que el mismo se ejecuta correctamente.
**Recomendación:** No cerrar la sesión de root ya que nos puede servir en caso de que algo esté mal configurado)
6. Ya tenemos listo nuestro servidor. Procedemos a instalar docker y docker-compose. Para ello, recomiendo consultar las guias oficiales. 
* Docker: https://docs.docker.com/engine/install/ubuntu
* Docker compose: https://docs.docker.com/compose/install/
7. Clonar el repositorio en el directorio deseado.
8. Ubicarse dentro del directorio del repositorio, donde se encuentra el archivo docker-compose.yml. Para realizar el primer despliegue de la aplicación ejecutamos **docker-compose up --build** De aquí en mas no será necesario el flag *--build* 

Habiendo desplegado la aplicación podemos ingresar desde nuestro navegador ingresando la ip públida de nuestro droplet, y puerto 3000 para frontend y 8000 para backend

ISSUES: 
* Al presionar el boton de solicitud de préstamos, no se puede conectar al host endpoint.test.com.ar:7001
* Se ha modificado frontend/src/index.js de forma tal que no tenemos error CORS. Sin embargo, al consultar la API se recibe un error 401 (no autorizado)
* Al ejecutarse el servicio backend quedan migraciones por realizar
* Al desplegar en un droplet podemos ingresar al servicio de backend, pero no el frontend reporta un  *Error net::ERR_ADDRESS_INVALID*