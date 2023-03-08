# Entrega 4

Repositorio con código base para la implementación de MS logistica haciendo uso de eventos.

## Estructura del proyecto

A continuación puede ver la nueva estructura:

- El directorio **src/integracion_logistica/** incluye las clases y archivos que constituyen el contexto con la integración con los servicios de logistica.
- El directorio **src/pagos/** ahora incluye todas las clases y archivos que constituyen el contexto de pagos.
- El proyecto `alpesonline` acontiene configuracion inicial de db.

## AlpesOnline
### Ejecutar Base de datos
Desde el directorio principal ejecute el siguiente comando.

```bash
docker-compose --profiles db up
```

### Ejecutar pruebas

```bash
coverage run -m pytest
```

### Ver reporte de covertura
```bash
coverage report
```

### Crear imagen Docker

Desde el directorio principal ejecute el siguiente comando.

```bash
docker build . -f alpesonline.Dockerfile -t alpesonline/flask
```

### Ejecutar contenedora (sin compose)

Desde el directorio principal ejecute el siguiente comando.

```bash
docker run -p 5000:5000 alpesonline/flask
```

## Sidecar/Adaptador
### Instalar librerías

En el mundo real es probable que ambos proyectos estén en repositorios separados, pero por motivos pedagógicos y de simpleza, 
estamos dejando ambos proyectos en un mismo repositorio. Sin embargo, usted puede encontrar un archivo `sidecar-requirements.txt`, 
el cual puede usar para instalar las dependencias de Python para el servidor y cliente gRPC.

```bash
pip install -r sidecar-requirements.txt
```

### Ejecutar Servidor

Desde el directorio principal ejecute el siguiente comando.

```bash
python src/sidecar/main.py 
```

## Microservicio: Integración Logistica

Desde el directorio `src` ejecute el siguiente comando

```bash
uvicorn integracion_gds.main:app --host localhost --port 8002 --reload
```

### Instrucciones oficiales

Para seguir la guía oficial de instalación y uso de Debezium en Apache Pulsar puede usar el siguiente [link](https://pulsar.apache.org/docs/2.10.x/io-cdc-debezium/)


## Docker-compose

Para desplegar toda la arquitectura en un solo comando, usamos `docker-compose`. Para ello, desde el directorio principal, ejecute el siguiente comando:

```bash
docker-compose up
```

Si desea detener el ambiente ejecute:

```bash
docker-compose stop
```

En caso de querer desplegar dicha topología en el background puede usar el parametro `-d`.

```bash
docker-compose up -d
```

## Comandos útiles

### Listar contenedoras en ejecución
```bash
docker ps
```

### Listar todas las contenedoras
```bash
docker ps -a
```

### Parar contenedora
```bash
docker stop <id_contenedora>
```

### Eliminar contenedora
```bash
docker rm <id_contenedora>
```

### Listar imágenes
```bash
docker images
```

### Eliminar imágenes
```bash
docker images rm <id_imagen>
```

### Acceder a una contendora
```bash
docker exec -it <id_contenedora> sh
```

### Kill proceso que esta usando un puerto
```bash
fuser -k <puerto>/tcp
```

### Correr docker-compose usando profiles
```bash
docker-compose --profile <pulsar> up
```