# Lab 3.3 - Advanced Warehouse Setup with AWS RedShift and RedShift Spectrum

This guide provides detailed instructions for advanced implementation of a data warehouse using Amazon RedShift and RedShift Spectrum. Assuming the basic infrastructure on RedShift, AWS S3, AWS Glue, and Amazon Athena is already set up (see [Previous Laboratory](https://github.com/jdprietom03/jdprietom-st0263/blob/main/lab%203-2/ReadMe.md)), we will proceed with configuring the warehouse.

## Steps

### 1. IAM Role Configuration

#### 1.1 Defining the Role
Navigate to the IAM (Identity and Access Management) service as shown in the image:

<img width="602" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b8a84b11-0cde-405a-ab62-ce4445acf33b">

Then, go to the Access Management >> Roles section:

<img width="375" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/4f0d1297-817b-4b8a-9957-37295cda5aac">

Once there, click on Create Role:

<img width="394" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/18190b73-6ea3-45b0-af47-f3dba2c34e32">

Here, set up our role for the entity type ```AWS Service```:

<img width="601" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/fa6b9b32-82bb-45f1-8fd6-d2cfeccbf21a">

Select the ```Redshift``` service:

<img width="605" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/e939d4cc-35fa-4e3b-8d72-2b41ac242595">

Finally, choose the case ```Redshift - Customizable```.

#### 1.2 Defining Permission Policies
Next, define the Permission Policies from the following list:

<img width="602" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/d1d60228-3be8-411e-a17f-82c6b899b6ea">

Select the permissions as shown:

<img width="613" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/8406c116-a747-4879-9a06-bad3262bdb97">

#### 1.3 Naming Our Role
Now assign a name to our Role:

<img width="602" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/75efb8ee-775d-4504-ae74-543ad6215fab">

#### 1.4 Validation and Confirmation
Double-check our information and finally click the ```Create Role``` button.

<img width="601" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/78be1e56-32d8-406f-bb93-30b0ae7c37ae">

#### 1.5 Obtaining Our Role's ARN
Once our role is created, return to the Roles section and find the role we created:

<img width="599" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/16a90943-3027-4386-b66f-cebc036b0ead">

In the Summary section, locate the ```ARN``` field and copy this value as it will be needed later.

<img width="589" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/227905e3-5ce2-4247-9d67-7b72f7a202c7">

---

Continuando con la documentación:

### 2. Utilizing RedShift's Query Editor Service

#### 2.1 Accessing the Query Editor - RedShift

To do this, access the RedShift service on AWS:

<img width="568" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/6559d3ab-fbb3-459b-8ca4-ac022705e478">

There, select your cluster:

<img width="599" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b9775199-f69c-4335-a11a-b9b2d423a741">

Proceed to the 'Query data' section and enter 'Query in query editor v2':

<img width="887" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/46868aea-d556-46fa-bae5-ad953f6fdd51">

Once in the editor, configure the connection to the service by entering the credentials of your cluster's database:

<img width="743" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/68ea1b5f-bd96-4723-8ee2-61d494dfa89d">

#### 2.2 Creating Our First External Database

Inside the editor, execute the following statement:

```SQL
create external schema myspectrum_schema
from data catalog
database '{database_name}'
iam_role '{role_arn}'
create external database if not exists;
```

For instance, it will appear as in the following image:

<img width="700" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/ae4099bb-e8cb-4921-9996-1c7d3df161c7">

Run the instruction, and it will create the database, showing a message like this:

<img width="700" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/12da928c-9be1-493d-811e-4c57dca49b06">

#### 2.3 Creating a Table with External Data in Our Database

##### 2.3.1 Preparing the Data

For this step, it's essential to have the bucket set up from the [previous lab](https://github.com/jdprietom03/jdprietom-st0263/blob/main/lab%203-2/ReadMe.md). The information it should contain is the [datasets](https://github.com/st1800eafit/st1800-232/tree/main/datasets) `tickitdb` and `tickitdb2/events` (importantly, `events` should be stored inside tickitdb).

##### 2.3.2 Creating the Table through Script

Once our data is stored in S3, run the following script in our editor (refer to the attached image):

```SQL
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
```

<img width="696" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/cf1f75c4-668d-48a7-87a1-77fb79329ec1">

After creation, we can see how many records were created in it with this instruction:

```SQL
select count(*) from myspectrum_schema.sales;
```

<img width="696" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/2e010601-3fc5-4345-b382-ed7c91b12897">


Continuing with the documentation:

### 2.4 Manipulating the Information in Tables

##### 2.4.1 Creating Native Tables
Next, we will create a native table in Redshift to combine it with the external table (refer to the attached image):

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

##### 2.4.2 Loading Data into Our New Table

Once our table is created, the next step is to load it with information from an external service (S3). The data we will load is from the `events` folder of the dataset (refer to the attached image).

```SQL
COPY my_native_table FROM '{s3_URI}'
iam_role '{iam_ARN}'
delimiter '|' timeformat 'YYYY-MM-DD HH:MI:SS' region 'us-east-1';
```

<img width="689" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b963c761-3e79-42fe-aa68-683748bdee58">

##### 2.4.3 Performing Operations on the Tables

Now that we have our two tables loaded with data, let's run a script to see information between them (refer to the attached image):

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

And that's it! This concludes the setup of the Warehouse with RedShift using external data from S3.
