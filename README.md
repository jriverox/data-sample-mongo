# Recursos para cargar data de ejemplo en bases de datos

## Propósito de este Repositorio

La idea de este repositorio es ayudar a aquellos que por razones de aprendizaje necesitan generar datos ya sea para una demo, práctica o un workshop.

Por ahora he creado un jason que contiene datos de contactos o personas ficticias y también indicaré como cargar esta data en MongoDB.

Espero en el futuro próximo colocar ejemplos útiles para MySQL, PostgreSQL, Elasticsearch, DynamoDB, etc.

## Tabla de Contenido

- [Propósito de este Repositorio](#propósito-de-este-repositorio)
  - [Tabla de Contenido](#tabla-de-contenido)
  - [Contactos esquema demo](#contactos-esquema-demo)
  - [Cómo cargar un Json según la BD](#cómo-cargar-un-json-según-la-bd)
    - [MongoDB](#mongodb)
      - [Usando Compass](#usando-compass)

## Contactos esquema demo

[Descarga el archivo de contactos aquí](./data/contacts-sample-data.json)

Contiene un arreglo de mas de 600 objetos con la siguiente estructura:

```json
 {
    "_id": "6224df1fecd9bb24050cf326",
    "index": 1,
    "dateOfBirth": "1994-01-01",
    "firstName": "Mcconnell",
    "lastName": "Pope",
    "username": "mcconnell.pope",
    "company": "Skybold",
    "email": "mcconnell.pope@skybold.com",
    "phone": "+1 432 106 4631",
    "address": {
      "street": "92 Roosevelt Place",
      "city": "Cuylerville",
      "state": "Indiana"
    },
    "jobPosition": "Executive",
    "roles": [
      "guest",
      "member"
    ],
    "active": true
  }
```

## Cómo cargar un Json según la BD

### MongoDB

El primer requisito es tener una BD en MongoDB, te recomiendo usar [MongoDB Atlas](https://www.mongodb.com/atlas/database), puedes registrarte y usarlo gratis sin necesidad de tarjetas de crédito, claro con almacenamiento limitado de hasta 500MB.

En caso de que quieras hacer una prueba de concepto rápida te sufiero usar MongoDB en un Contenedor Docker.

#### Correr MongoDB en Docker
Asegurate de tener instalado Docker y que se esté ejecutando.

Descarga la imagen de MongoDB
```bash
docker pull mongo
```
Una vez descargado la imagen desde docker hub, crea el contenedor
```bash
docker run --name mongodb-node-workshop -d -p 27017:27017 mongo
```
Listo con eso ya deberías poder conectarte desde Compass o algún GUI

**Nota:** Si apagas o reinicias la maquina puedes iniciar el contener con el siguiente comando:
```bash
docker start mongodb-node-workshop
```
Recuerda que en este ejemplo el nombre del contenedor es *mongodb-node-workshop* que fue el que usamos en el comando docker run, pero puedes usar el nombre de tu preferencia.

#### Usando Compass

[MongoDB Compass](https://www.mongodb.com/products/compass) es el cliente (GUI) oficial creado por MongoDB, aunque no suelo usarla mucho porque no me parece muy intuitiva prefiero usar [nosqlbooster](https://nosqlbooster.com/) pero para este caso de cargar data la versión free de NoSQLBooster no lo permite, debes tener la premium :-(

Entonces usemos Compass:

1. Abre Compass y en caso de que no tengas agregada la conexión deberás hacerlo primero. Recuerda que por ejemplo si estas ejecutando Mongo desde un contenedor docker local puede ser una conexión como: *mongodb://localhost:27017/* en caso de que no hayas establecido contraseña. O si estas usando un servidor en cloud por ejemplo en MongoDB Atlas es algo como *mongodb+srv://tu-usuario:tu-password@cluster0-8hxu4.mongodb.net/*

2. Has clic en el botón Connect.

<div align="center">
    <img src="images/01-mongo-compass-connection.jpeg"  width="50%">.
</div>

3. Selecciona en el panel izquierdo la Base de Datos y la Coleccion donde deseas cargar el json. También puedes crear una nueva Base de Datos y/o una nueva Coleccion en caso de que lo necesites.

<div align="center">
    <img src="images/02-panel-bds.jpeg"  width="40%">
</div>

4. Haz clic sobre la colección y selecciona los e puntos (...) y ahora Open in New Tab en caso de que no tengas abierto un tab de esa colección.

<div align="center">
    <img src="images/03-import-data.jpeg"  width="40%">
</div>

5. Se abrira una nueva ventana donde deberás seleccionar *Select a file...* y carga el archivo json.

<div align="center">
    <img src="images/04-modal-import-data.jpeg"  width="40%">
</div>

6. Haz clic en el botón *IMPORT*. Si todo salió bien veras un resultado como este:

<div align="center">
    <img src="images/05-import-data-done.jpeg"  width="40%">
</div>

Has cargado exitosamente la data en tu base de datos.
