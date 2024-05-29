# CONTENEDOR MONGODB + DUCKERHUB (CORRECCION POSIBLES ERRORES)
![Logo de mongo](https://www.openlogic.com/sites/default/files/image/2021-06/image-blog-openlogic-what-is-mongodb.png)

**Todos los comandos se realizan en el servidor de ubuntu mediante putty.**
## Paso 1 
### Crear documento de docker-compose.
> touch docker-compose.yml

> cat > docker-compose.yml
## Paso 2 
### Crear documento de docker-compose.yml:
*(copiamos y pegamos el codigo y al final guardamos con "ctrl+d")*

    version: '2.2'

    services:
    
      frontend:
  
        image: mongo:4.0.4
        
        restart: always
        
        ports:
        
          - "27017:27017"
        
        container_name: monguito
        
        environment:
        
          - MONGODB_USER='user'
         
          - MONGODB_PASS='pass'
        
        volumes:
        
          - monguitodata:/data/db
          
          - monguitologs:/var/log/mongodb/

    volumes:
    
      monguitodata:
      
      monguitologs:


## Paso 3
### Crear archivos para correr comando en la la terminal:
> touch mongo.sh
## Paso 4
### Cargar comandos al archivo creado:
> cat > mongo.sh

*(copiamos y pegamos el codigo y al final guardamos con "ctrl+d")*

    mkdir monguitodata && cd monguitodata; cd monguitodata || mkdir log
    cd
    sudo docker-compose up -d
    echo "Monguito está iniciandose ......."
    sudo docker exec -it monguito bash

## Paso 5
### Asignar permisos de ejecución y ejecutar mongo.sh
> chmod u+x mongo.sh

> ./mongo.sh 

Finalizamos con "exit".

---------------------------------------------------------------------------------------------------------------------------
**Pasos para la carga al repo de dockerhub**

## Paso 1
### Iniciar sesion
> sudo docker login -u *usuario_docker*

### Error 1 "docker login remote error from secret service..."

> sudo apt install gnupg2 pass
> sudo docker login -u *usuario_docker*

### Error 2 "Error response from daemon:..."
Nos dirigiremos a [docker](https://hub.docker.com)

* Iniciamos Sesion
* Arriba a la derecha picamos en "My account"
* Buscamos "security"
* En access token generamos uno nuevo con el nombre de preferencia
* Copiamos el token y lo ponemos en la contraseña
## Paso 2
### Crear archivo docker
> touch Dockerfile
> nano Dockerfile
## Paso 3
### Script para montar la imagen
    #Usa una imagen base oficial de MongoDB
    FROM mongo:latest
    
    #Copia el script mongo.sh en el contenedor
    COPY mongo.sh /docker-entrypoint-initdb.d/
    
    #Da permisos de ejecución al script
    RUN chmod +x /docker-entrypoint-initdb.d/mongo.sh
    
    #Comando por defecto para iniciar MongoDB
    CMD ["mongod"]
## Paso 4
 ### Crear imagen
 > docker build -t *usuario_docker*/mongo_*nombre_de_directorio* .

## Paso 5 
 ### Cargar imagen
 docker push *usuario_docker*/mongo_*nombre_de_directorio*

 ---------------------------------------------------------------------------------------------------------------------------
 ## Elaborado por:
 ### Gustavo Pardo Bermudez: TABOO52
 ### GITHUB
     https://github.com/TABOO52
 ### LINKEDIN
     www.linkedin.com/in/gustavo-pardo52

 ### AGRADECIMIENTO
 ![Logo de henry](https://assets.soyhenry.com/logoOG.png)
