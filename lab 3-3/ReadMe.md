# Lab 3.3 - Implementación de Warehouse con AWS Red Shift y RedShift Spectrum 

Después de configurar correctamente nuestra infrastructura en RedShift (Cluster), AWS S3, AWS Glue y Amazon Athenea ([Ver laboratio anterior](https://github.com/jdprietom03/jdprietom-st0263/blob/main/lab%203-2/ReadMe.md)) procederemos a la configuración del Warehouse.

## Pasos

### 1. Configuración de Role en IAM

#### 1.1 Definiendo el Role
Iremos al servicio de AIM, como lo muestra la imagen:

<img width="602" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b8a84b11-0cde-405a-ab62-ce4445acf33b">

Después, iremos al apartado de Access Managment >> Roles:

<img width="375" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/4f0d1297-817b-4b8a-9957-37295cda5aac">

Una vez dentro haremos clic en Create Role:

<img width="394" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/18190b73-6ea3-45b0-af47-f3dba2c34e32">

Aquí, configuraremos nuestro role para la entidad de tipo ```AWS Service```:

<img width="601" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/fa6b9b32-82bb-45f1-8fd6-d2cfeccbf21a">

Seleccionaremos el servicio ```Redshift```:

<img width="605" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/e939d4cc-35fa-4e3b-8d72-2b41ac242595">

Y por último escogemos el caso ```Redshift - Customizable```.

#### 1.2 Definiendo las Permission Policies
En el siguiente paso, vamos a definir las Permission Policies del siguiente listado:

<img width="602" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/d1d60228-3be8-411e-a17f-82c6b899b6ea">

Seleccionaremos los siguientes permisos:

<img width="613" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/8406c116-a747-4879-9a06-bad3262bdb97">

#### 1.3 Nombrando nuestro Role
Ahora asignaremos un nombre para nuestro Role:

<img width="602" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/75efb8ee-775d-4504-ae74-543ad6215fab">

#### 1.4 Validación y confirmación
Rectificamos nuestra información y por último le damos al botón ```Create Role```

<img width="601" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/78be1e56-32d8-406f-bb93-30b0ae7c37ae">

#### 1.5 Obtención del ARN de nuestro Role
Una vez se haya creado nuestro role, volvemos al apartado de Roles y buscaremos el que hemos creado:

<img width="599" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/16a90943-3027-4386-b66f-cebc036b0ead">

En el apartado de Summary encontraremos el campo ```ARN```, copiaremos este valor ya que nos servirá para más tarde.

<img width="589" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/227905e3-5ce2-4247-9d67-7b72f7a202c7">

---

### 2. Usando el servicio de Query Editor de RedShift
#### 2.1 Accediendo a Query Editor - RedShift

Para esto debemos acceder al sevicio de RedShift de AWS:

<img width="568" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/6559d3ab-fbb3-459b-8ca4-ac022705e478">

Allí, seleccionaremos nuestro cluster:

<img width="599" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b9775199-f69c-4335-a11a-b9b2d423a741">

Accederemos al apartado de ```Query data``` y accederemos a ```Query in query editor v2```:

<img width="887" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/46868aea-d556-46fa-bae5-ad953f6fdd51">

Una vez dentro del editor, vamos a configurar la conexión con el servicio ingresando con las credenciales de la base de datos de nuestro cluster:

<img width="743" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/68ea1b5f-bd96-4723-8ee2-61d494dfa89d">

#### 2.2 Creando nuestra primera base de datos externa

Una vez dentro de nuestro editor, podemos la siguiente sentencia:

```SQL
create external schema myspectrum_schema
from data catalog
database '{database_name}'
iam_role '{role_arn}'
create external database if not exists;
```

En nuestro caso, se verá como en la siguiente imágen:

<img width="700" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/ae4099bb-e8cb-4921-9996-1c7d3df161c7">

Correremos nuestra instrucción y nos creará la base de datos mostrandonos un mensaje como el siguiente:

<img width="700" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/12da928c-9be1-493d-811e-4c57dca49b06">

#### 2.3 Creando una tabla con datos externos en nuestra base de datos

##### 2.3.1 Preparando los datos

Para este paso es importante que dispongas del bucket configurado en el [laboratio anterior](https://github.com/jdprietom03/jdprietom-st0263/blob/main/lab%203-2/ReadMe.md). La información que debe contener son los [datasets](https://github.com/st1800eafit/st1800-232/tree/main/datasets) ```tickitdb``` y ```tickitdb2/events``` (es importante que ```events``` sea guardado dentro de tickidb).

##### 2.3.2 Creando la tabla mediante Script
Una vez tengamos guardados nuestros datos en el S3, correremos el siguiente script en nuestro editor (guiarse en la imágen adjunta):

````SQL
create external table myspectrum_schema.sales(
  salesid integer,
  listid integer,
  sellerid integer,
  buyerid integer,
  eventid integer,
  dateid smallint,
  qtysold smallint,
  pricepaid decimal(8,2),
  commission decimal(8,2),
  saletime timestamp)
  row format delimited
  fields terminated by '\t'
  stored as textfile
  location '{s3_URI}'
table properties ('numRows'='172000');
````

<img width="696" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/cf1f75c4-668d-48a7-87a1-77fb79329ec1">

Una vez creada podemos ver cuantos registros se crearon en la misma con esta instrucción:
```SQL
select count(*) from myspectrum_schema.sales;
```

<img width="696" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/2e010601-3fc5-4345-b382-ed7c91b12897">


### 2.4 Manipulando la información de las tablas

##### 2.4.1 Creando tablas nativas
A continuación, crearemos una tabla nativa en redshift para combinarla con la tabla externa (ver imágen adjunta):

```SQL
create table my_native_table(
  eventid integer not null distkey,
  venueid smallint not null,
  catid smallint not null,
  dateid smallint not null sortkey,
  eventname varchar(200),
  starttime timestamp
);
```

<img width="693" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/094b3982-b8e0-4d02-a23a-81b848efa457">

##### 2.4.2 Cargando datos en nuestra nueva tabla

Una vez creada nuestra tabla, el siguiente paso es cargarla de información proveniente de un servicio externo (S3). La información que vamos a cargar en su interior es la de la carpeta ```events``` del dataset (Ver imágen adjunta).

```SQL
COPY my_native_table FROM '{s3_URI}'
iam_role '{iam_ARN}'
delimiter '|' timeformat 'YYYY-MM-DD HH:MI:SS' region 'us-east-1';
```

<img width="689" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b963c761-3e79-42fe-aa68-683748bdee58">

##### 2.4.3 Aplicando operaciones sobre las tablas

Ahora que tenemos nuestras dos tablas con información cargada, vamos a correr un pequeño script para ver información entre ellas (Ver imágen adjunta):

```SQL
select top 10 myspectrum_schema.sales.eventid,
sum(myspectrum_schema.sales.pricepaid)
from myspectrum_schema.sales, my_native_table
where myspectrum_schema.sales.eventid = my_native_table.eventid
and myspectrum_schema.sales.pricepaid > 30
group by myspectrum_schema.sales.eventid
order by 2 desc;
```

<img width="886" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/8430c80e-08ac-437f-b60e-6a844578c04f">


Y listo, con esto concluimos la configuración del Warehouse con RedShift con datos externos de S3.
