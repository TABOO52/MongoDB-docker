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
