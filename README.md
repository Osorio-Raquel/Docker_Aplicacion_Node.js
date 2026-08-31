# Hello Node.js - Docker

## Nombre del estudiante

**Raquel Osorio**

## Descripción

Esta aplicación es un servidor web sencillo desarrollado con Node.js. La aplicación utiliza el módulo HTTP de Node.js para crear un servidor que responde a las solicitudes realizadas mediante un navegador o mediante la terminal.

El objetivo del proyecto es poner en práctica la creación de una imagen Docker utilizando un Dockerfile, ejecutar una aplicación Node.js dentro de un contenedor y realizar el mapeo de puertos entre el equipo local y el contenedor.

## Tecnologías utilizadas

- Node.js 20
- Docker
- Docker Alpine Linux
- JavaScript

## Estructura del proyecto

hello-node/
├── Dockerfile
├── index.js
├── package.json
├── package-lock.json
├── README.md
└── capturas/
    ├── docker-images.png
    ├── docker-ps.png
    └── aplicacion.png

## Aplicación

La aplicación inicia un servidor HTTP en el puerto 3000 y muestra el siguiente mensaje:

¡Hola desde Docker y Node.js!

El servidor está configurado para escuchar en 0.0.0.0, permitiendo que pueda ser accedido desde fuera del contenedor.

## Dockerfile

La imagen utilizada como base es:

node:20-alpine

El directorio de trabajo dentro del contenedor es:

/app

Primero se copia el archivo package.json y se ejecuta npm install. Posteriormente se copian los demás archivos de la aplicación.

Finalmente, se expone el puerto 3000 y se ejecuta la aplicación mediante npm start.

El contenido del Dockerfile es:

FROM node:20-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]

## Construcción de la imagen

Para construir la imagen Docker se utilizó:

docker build -t hello-node:1.0 .

Para comprobar que la imagen fue creada:

docker images

## Ejecución del contenedor

El contenedor fue ejecutado mediante:

docker run -d --name hello-node-container -p 8080:3000 hello-node:1.0

El puerto 8080 del equipo local se encuentra conectado con el puerto 3000 del contenedor.

PC                         CONTENEDOR
8080  ──────────────────►  3000

## Verificación del contenedor

Para comprobar que el contenedor se encuentra funcionando:

docker ps

## Aplicación funcionando

La aplicación puede ser consultada desde el navegador mediante:

http://localhost:8080

La aplicación muestra:

¡Hola desde Docker y Node.js!

## Comandos utilizados

### Construir imagen

docker build -t hello-node:1.0 .

### Ejecutar contenedor

docker run -d --name hello-node-container -p 8080:3000 hello-node:1.0

### Ver contenedores

docker ps

### Ver imágenes

docker images

### Ver logs

docker logs hello-node-container

### Detener contenedor

docker stop hello-node-container

### Eliminar contenedor

docker rm hello-node-container
