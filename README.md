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

ISSUES: 
* Al presionar el boton de solicitud de préstamos, no se puede conectar al host endpoint.test.com.ar:7001
* Se ha modificado frontend/src/index.js de forma tal que no tenemos error CORS. Sin embargo, al consultar la API se recibe un error 401 (no autorizado)
* Al ejecutarse el servicio backend quedan migraciones por realizar