# Instrucciones de como hacer la instalación de teemii, utilizando Docker

Ambiente: MacOS Apple Chip

1. Hacer la instalación de Docker en la máquina donde se van a hostear los contenedores. 
2. En este caso al ser un MacOS apple chip, se va a hacer uso de Brew, ejecutar el siguiente comando:

```
brew install docker
```

3. Una vez con docker instalado, crear un docker Network. Ejecutar el siguiente comando:

```
docker network create home-bridge -d bridge
//El comando anterior va a crear un docker network llamado 'home-bridge' y se le asignó el tipo bridge
```

4. Crear un volumen, esto va a ser utilizado para la persistencia de la data. Ejecutar el siguiente comando:

```
docker volume create teemii-data
```

5. Una vez completados los pasos anteriores, se debe de hacer pull de las imagenes tanto del frontend, como del backend para ser utilizadas. Ejecutar los siguientes comandos:

```
docker pull dokkaner/teemii-frontend:latest
docker pull dokkaner/teemii-backend:latest
```

6. Ya que se tienen las imagenes, para la creación de los contenedores. Proceder a correr ambos contenedores haciendo uso del docker network y volumen creado en pasos 3 y 4 respecivamente. 

```
//Backend primero
docker run -d --name teemii-backend --network home-bridge -v teemii-data:/data dokkaner/teemii-backend:latest

//Frontend
docker run -d -p 8080:80 --name teemii-frontend --network home-bridge dokkaner/teemii-frontend:latest
```

7. Verificar que ambos contenedores estén corriendo correctamente

```
docker ps
```

![docker_ps](https://github.com/KennethSV/Dockers/blob/main/docker%20containers%20creation.png)

8. Si completados los pasos anteriores correctamente, podrás ingresar a la aplicación yendo a la siguiente dirección: http://localhost:8080

9. Disfrutar!

![localhost](https://github.com/KennethSV/Dockers/blob/main/teemii%20running.png)
