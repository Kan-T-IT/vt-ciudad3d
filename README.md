## Vector Tiles Server

servidor liviando de tiles vectoriales a partir de arcchivos mbtiles

### Stack:
- expressJs
- sqlite
- docker
- pm2

## Directorio de datos
Se asume que hay un directorio principal montado en /data donde se agrupan las capas (mbtiles) según proyecto.

```
`-- /data/
    |-- grupo1/
        `-- capa1.mbtiles
        `-- capa2.mbtiles
    |-- grupo2/
        `-- capa1.mbtiles
        `-- capa2.mbtiles  
```

## Entorno de Producción:

Está pensado para correrlo con docker-compose, con un nginx que hace de proxy (con SSL) de instancias de node/express corriendo en cluster con pm2. 

Ajustar el docker-compose a gusto y:
```bash
$ docker-compose up
```
o para que quede corriendo
```bash
$ docker-compose up -d
```

### PM2 y monitoreo

comandos útiles

Command | Description
--------|------------
```$ docker exec -it <container-id> pm2 monit``` | Monitorear CPU/Uso de cada proceso
```$ docker exec -it <container-id> pm2 list``` | Listar los procesos 
```$ docker exec -it <container-id> pm2 show``` | Mas info de un proceso
```$ docker exec -it <container-id> pm2 reload all``` | recargar todas las aplicaciones


La doc de pm2 se encuentra [acá](http://pm2.keymetrics.io/docs/usage/docker-pm2-nodejs/).

## Entorno de Desarrollo:

Para hacer pruebas solo es necesario:
```bash
$ cd server
$ npm install
$ DEV=true node server.js 

```
Notar que se setea la variable de entorno **DEV**. En este modo se setea el directorio de datos en *./test_data*

siguiendo el ejemplo del directorio de datos se podrán servir capas en las siguientes urls:

- http://localhost:8080/grupo1/capa1/{z}/{x}/{y}.pbf
- http://localhost:8080/grupo1/capa2/{z}/{x}/{y}.pbf

