# Lab 3.2: SIMPLE DATA WAREHOUSE IMPLEMENTATION WITH AWS S3, GLUE, AND ATHENA

## 1. Configuring AWS S3
First, access the S3 service on AWS:

<img width="881" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/fa53c905-dd05-431c-a914-c5123f2d5f54">

### 1.1 Creating a Bucket
We will create a bucket and assign it a name:

<img width="898" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/96dac058-654e-42e5-9ec3-de4a8ff20547">

#### 1.1.1 Enabling Public Access

Next, we'll configure our bucket for public access. Select ```ACLs enabled```:

<img width="881" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/61f8d7e2-f6fa-4bf9-9bb4-bb23b936ca25">

Remove the public restriction:

<img width="897" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b2024920-e85b-41f1-baf6-d8a4df638538">

#### 1.1.2 Validation and Creation

Finally, create the bucket by clicking on ```Create bucket```:

<img width="882" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/10b98c19-63b0-42c6-88e2-d9064973c11a">

## 1.2 Manually Uploading Content to the Bucket

Go to ```S3 >> Buckets``` and locate our bucket:

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/4e5c2b4b-bebd-4d8d-a325-3becc7ddd8b5">

Click on Upload:

<img width="897" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/c798a0c5-5cf2-4bdc-90c6-854055e49c7f">

Manually upload each file and/or directory:

<img width="883" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/70283c7c-ecc5-4cd9-98eb-48af4790a4e8">

Confirm the upload, and the files will be stored in AWS S3.

## 2. Configuring AWS Glue

### 2.1 Defining the Data Source

Navigate to the AWS Glue service:

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/da0f885d-917a-4e90-bdac-462845727365">

Once inside, go to ```Data Catalog >> Crawlers```:

<img width="600" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/1c0c7cc4-f469-43c3-a6b7-0684ceda1527">

Click on ```Create Crawler```:

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/57a4da92-95ed-4c64-84b8-0238f1586cb1">

Assign a name to our new crawler:

<img width="893" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/0291ed48-62b0-4e87-b0d8-83f1bd75c4ec">

Define the data source for our Crawler:

<img width="890" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/48ea3833-8c54-4242-a044-22bd1455d722">

A modal will open, where we will search for the path of our S3 origin:

<img width="888" alt="image" src="https://github.com/jdprietom

03/jdprietom-st0263/assets/80794157/49f95da5-9fe8-4ad0-b9f4-ca369a902332">

<img width="897" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/cc9f1e74-1734-4a59-a3c2-db0d26fafe5c">

Finalize the setup with a ```Next```:

<img width="901" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/ce497502-fa07-4d97-8a5f-c09b15ed417a">

### 2.2 Security Settings
In the security settings, select our Role:

<img width="894" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/92e1cabe-3511-4e62-b5ef-fd77598ce24e">

Choose our database next, and finally click ```Next``` to create our crawler:

<img width="894" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/718df324-2de6-4f9c-9266-9948a7e6e0de">

We will have a successfully created crawler:

<img width="891" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/2a96eb34-713a-412d-aeec-78c420fef77f">

### 2.3 Table Generation by Our Crawler

Once our crawler is created, run it to generate the corresponding tables:

<img width="898" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/c9a1e35b-e4b0-4670-afee-6fb626e86379">

Go to Data Catalog > Databases > Tables:

<img width="464" alt "image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/37f1a683-f2d8-41ce-8248-83cd0175db4b">

Now, we can see the tables created by our crawler:

<img width="899" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/2d8cbec3-7081-4593-9c25-17f363a26685">

## 3. Configuring AWS Athena

Now we will set up Athena, for that, we go to the Athena service in AWS:

<img width="888" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/07851721-28a9-4226-8d7e-42e47e5206a3">

Go to ```Query Editor``` in Athena:

<img width="824" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/ede17d23-b58b-45e7-9b5e-7a496428a091">

And now configure the location of our results:

<img width="902" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/51dc756c-3f9c-4b3a-ae69-58621bacbd10">

Select the destination and save:

<img width="861" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/c9e67f3b-36c1-4a6a-8f7e-56a0e924f80c">

Now when we return to the Athena Editor, it will have loaded our tables:

<img width="272" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/8b132179-9abc-40ad-af3a-221ba8076e4c">

Run a query in Athena, and we can see the results of our tables:

<img width="880" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/d5b7c197-ef48-443b-adb5-75b3ace3ab68">
