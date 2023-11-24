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
