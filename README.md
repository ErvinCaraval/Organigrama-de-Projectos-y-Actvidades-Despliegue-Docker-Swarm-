# Despliegue de Proyecto con Docker Swarm

Este proyecto utiliza Docker Swarm para desplegar múltiples servicios que incluyen una aplicación web basada en Django, una base de datos PostgreSQL, un frontend y pruebas de carga con Locust.

## Requisitos Previos

- Docker Engine configurado para utilizar Docker Swarm
- Imágenes Docker disponibles para `ervincaravaliibarra/webbackend:latest`, `ervincaravaliibarra/dbbackend:latest` y `ervincaravaliibarra/frontend:latest`
- Archivo `.env` con las variables de entorno necesarias en el directorio raíz del proyecto

## Pasos para Desplegar el Entorno con Docker Swarm

1. **Inicializar Docker Swarm (si no está inicializado)**

   Si no has inicializado Docker Swarm en tu máquina, ejecuta el siguiente comando:

   ```sh
   docker swarm init

   ```

2. **Clonar el Repositorio**

   Clona este repositorio en tu máquina local:

   ```sh
   git clone https://github.com/tu_usuario/tu_repositorio.git
   cd tu_repositorio
   ```

3. **Configurar el Archivo `.env`**

   Crea un archivo `.env` en la raíz del proyecto y agrega las siguientes variables de entorno con los valores correspondientes:

   ```env
   DB_HOST=db
   DB_NAME=nombre_de_tu_bd
   DB_USER=usuario_de_tu_bd
   DB_PASSWORD=contraseña_de_tu_bd
   ```

4. **Desplegar los Servicios con Docker Stack**

   Utiliza el siguiente comando para desplegar los servicios definidos en el archivo `docker-compose.yml` como un stack en Docker Swarm:

   ```sh
   docker stack deploy -c docker-compose.yml proyecto_stack
   ```

   Reemplaza `proyecto_stack` con el nombre que desees para tu stack.

5. **Ver el Estado de los Servicios**

   Para verificar el estado de los servicios desplegados, utiliza el siguiente comando para ver los detalles de cada réplica del stack:

   ```sh
   watch -n 3 'docker stack ps proyecto_stack'
   ```

6. **Acceder a la Aplicación Web**

   Una vez que los servicios estén desplegados, puedes acceder a la aplicación web en tu navegador en la siguiente URL:

   ```
   http://localhost:8000
   ```

7. **Acceder al Frontend**

   El frontend está disponible en:

   ```
   http://localhost:5173
   ```

8. **Acceder a la Base de Datos PostgreSQL**

   La base de datos PostgreSQL está disponible en el puerto 5433 de tu máquina local. Puedes conectarte a ella usando cualquier cliente de base de datos PostgreSQL.

9. **Ejecutar Pruebas con Locust**

   Para ejecutar las pruebas de carga con Locust, abre tu navegador y dirígete a:

   ```
   http://localhost:8090
   ```

10. **Eliminar Servicios y Limpiar Imágenes**

    Para limpiar y eliminar servicios y contenedores:

    ```sh
    docker service rm $(docker service ls -q)
    docker rmi $(docker images -f "dangling=true" -q)
    ```

## Servicios Definidos en `docker-compose.yml`

- **web**: Servicio que ejecuta la aplicación Django.
- **db**: Servicio que ejecuta la base de datos PostgreSQL.
- **frontend**: Servicio que ejecuta el frontend de la aplicación.
- **tests**: Servicio que ejecuta las pruebas de carga con Locust.

## Detalles Técnicos

- Cada servicio está configurado para tener una réplica (`replicas: 1`) y utilizar una política de reinicio flexible (`restart_policy: any`).
- Los servicios están configurados para utilizar variables de entorno definidas en el archivo `.env`.
- Los volúmenes son gestionados por Docker Swarm para garantizar la persistencia de datos.

## Comandos Útiles de Docker Swarm

- **Ver el estado del stack**:

  ```sh
  docker stack ps proyecto_stack
  ```

- **Detener y eliminar el stack**:

  ```sh
  docker stack rm proyecto_stack
  ```

## Solución de Problemas

- Verifica las credenciales de la base de datos en el archivo `.env` si encuentras problemas de conexión.
- Asegúrate de que los puertos necesarios (8000, 5433, 5173 y 8090) estén disponibles en tu máquina local.

## Contacto

Para cualquier pregunta o problema, por favor abre un issue en el repositorio o contacta directamente.

¡Gracias por utilizar este proyecto con Docker Swarm!
```

Este archivo `README.md` proporciona todas las instrucciones necesarias para configurar, desplegar y gestionar tu proyecto utilizando Docker Swarm en un formato continuo y completo. 
