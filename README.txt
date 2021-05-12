///   DEVELOPMENT  ///
Para crear la imagen usaremos el siguiente comando:
  docker build -f Dockerfile.dev .

Arrancaremos la imagen con:
  -Linux: docker run -p 3000:3000 -v /usr/app/node_modules -v $(pwd):/usr/app <imgId>

  -Windows: docker run -it -p 3000:3000 -v /usr/app/node_modules -v "/d/workspace pruebas/udemy/docker/prod-gradle-workflow/frontend":/usr/app -e CHOKIDAR_USEPOLLING=true  <imgId>

  Lo que esta haciendo es crear referenceas del directorio actual, cogiendo del comando pwd, y asignandolo al espacio del contenedor /usr/app 
  en vez de copiarlos directamente dentro de la imagen. /usr/app es nuestro WORKDIR indicado en el dockerfile

  -v (directorio local:directorioContenedor)

  En el caso de node_modules, solo hacemos un etiquetado de la carpeta que ya contiene la imagen al desplegarse

Ejecutar los test

  Se puede hacer ejecutando el siguiente comando
    - npm exec -it <containerId> npm run test

//// CON DOCKER COMPOSE ///
  La configuracion es igual que en el caso anterior, solo que se configura todo el en docker-compose.yaml

  Arrancamos el compose con: docker compose up


  ///PRODUCTIO

  Al generar la imagen y montar la distribución sobre el nginx deberemos de arrancar con

  docker run -p 8080:80 <imgId>
