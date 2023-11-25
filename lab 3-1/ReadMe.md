# Lab 3.1: File Management in HDFS and S3

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

<img width="892" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/283f0d02-3a9f-40b3-886d-cdf3882cbc20">

Confirm the upload, and the files will be stored in AWS S3.

A continuación entramos a nuestro archivo ya cargado y accederemos al link del ```Object URL```:

<img width="1662" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/f661edc1-32dd-4842-9326-50f0f50c3a2a">

Veremos el siguient mensaje al intentar acceder:

<img width="1010" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/5e99c942-b504-4a83-847a-29d522b28416">

✅ You're done! You now have an AWS S3 public bucket.

Note: In order to read the files from the public bucket created above through the AWS CLI you can use the following command:

```bash
aws s3 ls s3://<YOUR_BUCKET_NAME>
```
Command to read the previously created bucket

```bash
aws s3 ls s3://jdprietom03
```
<img width="706" alt="image" src="https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/6087b263-5b88-4151-b418-17a273eb331e">

---

### Section 2: File management in HDFS using terminal

1. We will have to create an AWS EMR cluster, visit the following guide '[Creating an EMR Cluster](https://github.com/st0263eafit/st0263-232/blob/main/bigdata/00-lab-aws-emr/Install-AWS-EMR.pdf)' for this purpose.
2. Once the cluster specified above has been created we must connect to it via SSH; how to connect to the cluster via SSH can be found
2.1 Access to Primary node

2.1.1. Within the Amazon EMR menu go to **Clusters** and select the `Cluster ID` that has the create before.

2.1.2. Click on the URL ```Connect to the Primary node using SSM``` and follow the instructions there. 
    
<img width="1567" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/c7d53aef-fcec-4338-9da4-1b44f5f79f71">

2.1.3. A successful SSH connection to the master node of the cluster will look as follows:
    
<img width="623" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/56d34303-2972-46f2-80d0-7e58bdaef4f5">

2.1.4. You will need to edit the 'hue.ini' file by following these steps: 

2.1.4.1. Type the following command in the terminal:

```bash
sudo nano /etc/hue/conf/hue.ini
```
    
2.1.4.2. Find the line containing 'webhdfs_url' and change the port. You should put the HDFS Name Node port found in the Applications section over your cluster.

<img width="624" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/d5d797bc-ef9d-4341-8075-d277cf321b0b">

As you can see, the selected port must be 9870
        
<img width="620" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/ac5a3857-5d64-4404-8746-f1df054f820d">
        
2.1.4.3. Save the changes over the file.

2.1.4.4. Restart the Hue service using the following command:
    
```bash
sudo systemctl restart hue.service
```
        
4. After establishing a connection to the primary node we will create a folder called 'gutenberg-small' inside the path '/user/hadoop/datasets' using the following commands:

1. Create the directory 'datasets' inside the path 'user/hadoop/'.

```bash
hdfs dfs -mkdir /user/hadoop/datasets
```

2. Create the directory 'gutenber-small' inside the path 'user/hadoop/datasets/'.

```bash
hdfs dfs -mkdir /user/hadoop/datasets/gutenberg-small
```

3. List directories and files present in /user/hadoop/ path

```bash
hdfs dfs -ls /user/hadoop/datasets
```
    
5. Put the contents of a local to the directory '/user/hadoop/datasets/gutenberg-small' using the following command. For this purpouse you could clone the repository that has example datasets
    
    ```bash
    hdfs dfs -put <YOUR_LOCAL_FOLDER> /user/hadoop/datasets/gutenberg-small/
    ```

✅ You are done! You can now manage files to HDFS from the EMR cluster using the terminal.

---

### Section 3: File management in HDFS using HUE

1. Go to AWS console and search for the EMR service.
2. Select the 'Cluster ID' that has the status 'Waiting'; then select the **Applications** option.
3. Select the URL of the **Hue** field and enter the 'hadoop' user and a password.
4. Select the **Files** section:
   
    <img width="820" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/a0ef39ee-0773-4d16-8baf-3d96ea237677">

6. If you have been following the previous steps right, you must found the folder **datasets**. Otherwise, create the folder in `New` button:
    
    <img width="820" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/b41c4eb2-df2f-4c83-bf1b-1f30fb1e73c6">
    
7. Select the `Upload` button:
    
    <img width="820" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/895a21a4-4d45-435c-be9d-0492ad517efc">

✅ Done! You can now upload files to HDFS of the EMR cluster via HUE.

---

### Section 4: File management in S3 using HUE

1. Log into the AWS console and search for the EMR service.
2. Select the 'Cluster ID' that has the status 'Waiting'; then select the '**Applications**' option.
3. Select the URL of the 'HUE' field and enter the 'hadoop' user and a password of your choice.
4. Select the **S3** section:
    
    <img width="820" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/70ca831c-62ce-4a67-a46f-15e4b78a3209">

5. All your buckets must be found there.

6. Select a bucket. Then, click on `Upload` button, `Select Files`; and finally choose the files you want to upload.

7. Verify the file is accesible through other ways like AWS CLI. Execute the next command to list the file over your bucket:

    ```bash
    aws s3 ls s3://<YOUR_BUCKET_NAME>
    ```

    Should show the file you uploaded before.

    <img width="820" alt="image" src="https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/59aa1ab6-7111-42da-b467-7b2a3ed5781e">

✅ Done! You can now upload files to an S3 bucket via HUE.

