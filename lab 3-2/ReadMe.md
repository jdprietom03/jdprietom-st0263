# Lab 3.2: IMPLEMENTACIÓN DE UN DATA WAREHOUSE SENCILLO CON AWS S3, GLUE y ATHENA.

## 1. Configurando AWS S3
Para esto debemos acceder al servicio de S3 en AWS:

<img width="881" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/fa53c905-dd05-431c-a914-c5123f2d5f54">

### 1.1 Creando un bucket
Crearemos un bucket y le asignaremos un nombre:

<img width="898" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/96dac058-654e-42e5-9ec3-de4a8ff20547">

#### 1.1.1 Habilitando acceso publico

Ahora configuraremos nuestro bucket para que pueda ser accedido por todos. Para esto debemos seleccionar ```ACLs enabled```:

<img width="881" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/61f8d7e2-f6fa-4bf9-9bb4-bb23b936ca25">

Quitamos la restricción de público:

<img width="897" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b2024920-e85b-41f1-baf6-d8a4df638538">

#### 1.1.2 Validamos y creamos

Y finalizamos creando el bucket (```Create bucket```):

<img width="882" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/10b98c19-63b0-42c6-88e2-d9064973c11a">

## 1.2 Subiendo contenido manualmente al bucket

Iremos al apartado de ```S3 >> Buckets``` y buscaremos nuestro bucket:

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/4e5c2b4b-bebd-4d8d-a325-3becc7ddd8b5">

Le daremos en Upload:

<img width="897" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/c798a0c5-5cf2-4bdc-90c6-854055e49c7f">

Cargamos manualmente cada uno de los archivos y/o directorios que queramos subir:

<img width="883" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/70283c7c-ecc5-4cd9-98eb-48af4790a4e8">

Confirmamos y quedarán subidos nuestros archivos en AWS S3.

## 2. Configurando  AWS Glue

### 2.1 Definiendo el origen de la información

Para esto debemos dirigirnos al servicio de AWS Glue:

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/da0f885d-917a-4e90-bdac-462845727365">

Una vez dentro, nos iremos al apartado de ```Data Catalog >> Crawlers```:

<img width="600" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/1c0c7cc4-f469-43c3-a6b7-0684ceda1527">

Le damos a ```Create Crawler```:

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/57a4da92-95ed-4c64-84b8-0238f1586cb1">

Le asignamos un nombre a nuestro nuevo crawler:

<img width="893" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/0291ed48-62b0-4e87-b0d8-83f1bd75c4ec">

Ahora le vamos a definir el origen de la información a procesar de nuestro Crawler:

<img width="890" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/48ea3833-8c54-4242-a044-22bd1455d722">

Nos abrirá una modal en la cual buscaremos el path de nuestro origen de S3:

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/49f95da5-9fe8-4ad0-b9f4-ca369a902332">

<img width="897" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/cc9f1e74-1734-4a59-a3c2-db0d26fafe5c">

Finalizamos la carga con un ```Next```:

<img width="901" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/ce497502-fa07-4d97-8a5f-c09b15ed417a">

### 2.2 Configuraciones de seguridad
En los ajustes de seguridad seleccionaremos nuestro Role:

<img width="894" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/92e1cabe-3511-4e62-b5ef-fd77598ce24e">

Seleccionaremos nuestra base de datos a continuación y por último le damos a ```Next``` para crear nuestro crawler:

<img width="894" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/718df324-2de6-4f9c-9266-9948a7e6e0de">

Tendremos un crawler creado con éxito:

<img width="891" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/2a96eb34-713a-412d-aeec-78c420fef77f">


### 2.3 Generación de tablas por nuestro Crawler

Ya creado nuestro crawler, lo vamos a correr para que genere las tablas correspondientes:

<img width="898" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/c9a1e35b-e4b0-4670-afee-6fb626e86379">

Ahora nos iremos a Data Catalog > Databases > Tables: 

<img width="464" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/37f1a683-f2d8-41ce-8248-83cd0175db4b">

Ahora podremos ver las tablas creadas por nuestro crawler:

<img width="899" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/2d8cbec3-7081-4593-9c25-17f363a26685">

## 3. Configurando AWS Athena

Ahora configuraremos Athena, para eso iremos al servicio de Athena en AWS

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/07851721-28a9-4226-8d7e-42e47e5206a3">

Iremos a ```Query Editor``` dentro de Athena:

<img width="824" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/ede17d23-b58b-45e7-9b5e-7a496428a091">

Y ahora configuraremos la ubicación de nuestros resultados:

<img width="902" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/51dc756c-3f9c-4b3a-ae69-58621bacbd10">

Seleccionamos el destino y guardamos:

<img width="861" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/c9e67f3b-36c1-4a6a-8f7e-56a0e924f80c">

Ahora cuando volvamos a Athena Editor tendrá cargadas nuestras tablas:

<img width="272" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/8b132179-9abc-40ad-af3a-221ba8076e4c">

Corremos una consulta en Athena y podremos ver los resultados de nuestras tablas:

<img width="880" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/d5b7c197-ef48-443b-adb5-75b3ace3ab68">
