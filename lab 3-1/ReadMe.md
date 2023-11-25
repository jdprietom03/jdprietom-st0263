# Lab 3.1: Comprehensive Guide for File Management in AWS S3

## Section 1: Configuring AWS S3 for Storage Operations

### Step 1.1: Initializing S3 Bucket
- **Access S3 Service**: Begin by accessing the AWS S3 service.

  ![Access S3 Service](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/fa53c905-dd05-431c-a914-c5123f2d5f54)

- **Bucket Creation**: Proceed to create a new S3 bucket and assign a unique name.

  ![Create Bucket](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/96dac058-654e-42e5-9ec3-de4a8ff20547)

#### Configuring Public Access
- **ACLs Configuration**: Enable 'ACLs' for public access settings.

  ![Enable ACLs](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/61f8d7e2-f6fa-4bf9-9bb4-bb23b936ca25)

- **Removing Public Restriction**: Adjust settings to remove the public access restriction.

  ![Remove Restriction](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b2024920-e85b-41f1-baf6-d8a4df638538)

- **Bucket Finalization**: Conclude the process by creating the bucket.

  ![Finalize Bucket](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/10b98c19-63b0-42c6-88e2-d9064973c11a)

### Step 1.2: Uploading Data to S3 Bucket
- **Navigating to Bucket**: Locate your bucket under 'S3 >> Buckets'.

  ![Locate Bucket](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/4e5c2b4b-bebd-4d8d-a325-3becc7ddd8b5)

- **Initiating Upload**: Select 'Upload' to start transferring files.

  ![Start Upload](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/c798a0c5-5cf2-4bdc-90c6-854055e49c7f)

- **File Selection**: Choose and upload the desired files or directories.

  ![Choose Files](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/283f0d02-3a9f-40b3-886d-cdf3882cbc20)

- **Accessing Uploaded Files**: Navigate to the uploaded file and access its 'Object URL'.

  ![Access Object URL](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/f661edc1-32dd-4842-9326-50f0f50c3a2a)

- **Public Access Verification**: Confirm the public accessibility of the file.

  ![Public Access Verification](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/5e99c942-b504-4a83-847a-29d522b28416)

#### AWS CLI Integration
- **Listing Files via CLI**: Utilize AWS CLI commands for file listing.

  ```bash
  aws s3 ls s3://<YOUR_BUCKET_NAME>
  ```

  ![CLI Command](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/6087b263-5b88-4151-b418-17a273eb331e)

✅ Successfully created a publicly accessible AWS S3 bucket.

---

# Lab 3.1: Comprehensive Guide for File Management in Hadoop Distributed File System (HDFS)

## Section 2: File Management in HDFS using Terminal

### Step 2.1: Creating and Accessing AWS EMR Cluster
- **Cluster Creation**: For the initial setup, create an AWS EMR cluster by referring to the '[Creating an EMR Cluster](https://github.com/st0263eafit/st0263-232/blob/main/bigdata/00-lab-aws-emr/Install-AWS-EMR.pdf)' guide.

### Step 2.2: SSH Connection to Cluster
- **Accessing the Primary Node**: In Amazon EMR, select your newly created cluster and navigate to 'Clusters >> Cluster ID'.

- **Connecting to Node**: Follow the detailed instructions under 'Connect to the Primary node using SSM'.

  ![Connect to Node](https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/c7d53aef-fcec-4338-9da4-1b44f5f79f71)

- **SSH Connection Verification**: A successful SSH connection to the master node of the cluster should resemble the following:

  ![SSH Connection](https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/56d34303-2972-46f2-80d0-7e58bdaef4f5)

#### Step 2.2.1: Editing 'hue.ini' File
- **Editing Configuration File**: To edit the 'hue.ini' file, execute the command `sudo nano /etc/hue/conf/hue.ini` in the terminal.

- **Modifying 'webhdfs_url'**: Locate and change the 'webhdfs_url' line to match the HDFS Name Node port found in the Applications section of your cluster.

  ![Edit hue.ini](https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/d5d797bc-ef9d-4341-8075-d277cf321b0b)

  The selected port should be 9870.

  ![Port Selection](https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/ac5a3857-5d64-4404-8746-f1df054f820d)

- **Saving Changes and Restarting Service**: After making the necessary changes, save the file and restart the Hue service using `sudo systemctl restart hue.service`.

### Step 2.3: Directory Creation and Data Transfer in HDFS
- **Creating Directories in HDFS**:
  - Command to create '/user/hadoop/datasets': `hdfs dfs -mkdir /user/hadoop/datasets`.
  - Command to create '/user/hadoop/datasets/gutenberg-small': `hdfs dfs -mkdir /user/hadoop/datasets/gutenberg-small`.

- **Listing Directories**: To view the directories, use `hdfs dfs -ls /user/hadoop/datasets`.

- **Transferring Data to HDFS**: Employ the `hdfs dfs -put` command to transfer local data to '/user/hadoop/datasets/gutenberg-small/'.

  ```bash
  hdfs dfs -put <YOUR_LOCAL_FOLDER> /user/hadoop/datasets/gutenberg-small/
  ```

✅ Completion of file management in HDFS using the terminal is now achieved. This section provides a step-by-step process to efficiently manage and transfer files within HDFS using an AWS EMR cluster.

---

# Lab 3.1: Comprehensive Guide for File Management in HDFS using HUE

## Section 3: File Management in HDFS via HUE

This section outlines the process of managing files in the Hadoop Distributed File System (HDFS) using the HUE interface on an AWS EMR cluster.

### Step 3.1: Accessing HUE on AWS EMR
1. **Navigating to EMR Service**: Start by logging into the AWS console and accessing the EMR service.

2. **Cluster Selection**: Choose the 'Cluster ID' of the EMR cluster that is in 'Waiting' status.

3. **Accessing HUE**: Locate the URL provided under the **Applications** tab for the HUE interface.

4. **Login Credentials**: Enter the platform using the 'hadoop' user credentials.

### Step 3.2: Uploading Files to HDFS
1. **Navigating to Files Section**: Within HUE, select the **Files** section to access HDFS directories and files.

   ![Files Section in HUE](https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/a0ef39ee-0773-4d16-8baf-3d96ea237677)

2. **Directory Verification**: If you have followed previous steps correctly, you should locate the **datasets** folder. If not present, create it using the `New` button.

   ![Create Folder](https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/b41c4eb2-df2f-4c83-bf1b-1f30fb1e73c6)

3. **Uploading Files**: Use the `Upload` button to transfer desired files from your local system to the HDFS directory.

   ![Upload Files](https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/895a21a4-4d45-435c-be9d-0492ad517efc)

✅ You have successfully uploaded files to HDFS using the HUE interface on an AWS EMR cluster.

---

# Lab 3.1: Comprehensive Guide for File Management in S3 using HUE

## Section 4: Managing Files in S3 via HUE

This section describes the process of managing and uploading files to Amazon S3 buckets using the HUE interface within an AWS EMR cluster.

### Step 4.1: Accessing HUE for S3 File Management
1. **EMR Service Access**: Log into the AWS console and navigate to the EMR service.

2. **Cluster Selection**: Choose the 'Cluster ID' of your EMR cluster that is in the 'Waiting' state.

3. **HUE Interface**: Select the 'HUE' field URL under the '**Applications**' tab.

4. **HUE Login**: Enter the interface using the 'hadoop' user credentials.

### Step 4.2: Uploading Files to S3 via HUE
1. **Navigating to S3 Section**: In the HUE interface, go to the **S3** section to access your AWS S3 buckets.

   ![S3 Section in HUE](https://github.com/Jguerra47/jsguerrah-st0263/assets/68879896/70ca831c-62ce-4a67-a46f-15e4b78a3209)

2. **Bucket Selection**: All your S3 buckets should be visible here. Select the desired bucket for file management.

3. **File Upload Process**: Click on the `Upload` button, then `Select Files` to choose and upload files from your local system to the chosen S3 bucket.

4. **AWS CLI Verification**: To confirm the file's presence, use the AWS CLI command to list the contents of your bucket:

    ```bash
    aws s3 ls s3://<YOUR_BUCKET_NAME>
    ```

    This command should display the recently uploaded file.

   ![CLI Verification](https://github.com/jdprietom03/jdprietom-st0263/assets/80794157/b87f976d-3dee-4516-8093-08cb2f736fad)

✅ You have now successfully managed and uploaded files to an S3 bucket via the HUE interface on an AWS EMR cluster.
