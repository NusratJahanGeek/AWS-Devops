# Lab - 1
## Introduction to Amazon Simple Storage Service (S3)

Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means customers of all sizes and industries can use it to store and protect any amount of data for a range of use cases, such as websites, mobile applications, backup and restore, archive, enterprise applications, Internet of Things (IoT) devices, and big data analytics. Amazon S3 provides easy-to-use management features so you can organize your data and configure finely-tuned access controls to meet your specific business, organizational, and compliance requirements. Amazon S3 is designed for 99.999999999% (11 9’s) of durability and stores data for millions of applications for companies all around the world.

## Lab Scenario

Assuming I work for a company using Amazon S3 for data storage. An application residing on an EC2 instance needs to push reporting data to an S3 bucket daily. I am tasked with creating an S3 bucket for my company to use for storing this report data. For a successful deployment, I need to ensure the EC2 instance has enough privileges to upload and retrieve data from the S3 bucket. For security reasons, only the EC2 instance can write data to the S3 bucket. The files in the S3 bucket also require protection against accidental deletion.

## Objective - 1: Create a Bucket in Amazon S3

I am new to Amazon S3 and want to test its features and security as I configure the environment to hold the EC2 report data. Since every object in Amazon S3 is stored in a bucket, creating a new bucket to hold the reports is the first task on my list.

In this task, I'll create a bucket to hold my EC2 report data and then examine the different bucket configuration options.

![Create Bucket](https://github.com/user-attachments/assets/24a77311-cc1d-4dfb-bf48-11fffbe7893f)

## Objective - 2: Upload an Object to the Bucket

An object can be any kind of file: a text file, a photo, a video, a zip file, and so on. When I add an object to Amazon S3, I have the option to include metadata with the object and set permissions to control access.

![Upload Object](https://github.com/user-attachments/assets/e88626ef-55c5-4de8-8963-84ba43785094)

## Objective - 3: Manage Access Permissions on an Object and a Bucket

Security is a priority in Amazon S3. Before I configure my EC2 instance to connect to the report bucket, I want to test the bucket and object settings for security.

The uploaded file showed an 'access denied' error. This is because objects in Amazon S3 are private by default.

![Access Denied](https://github.com/user-attachments/assets/cd1af3e6-2733-4e62-b579-8f0745b3909c)

### Steps Taken:
1. **First, I updated the "Block Public Access" settings:**

   ![Block Public Access](https://github.com/user-attachments/assets/f86d8f88-dfbe-41a3-a412-1ec8da4a73aa)

2. **Then, I made the object publicly accessible by clicking on "Make public via ACL":**

   ![Make Public via ACL](https://github.com/user-attachments/assets/13ea9234-c62a-42b4-9846-0e414f8dbcec)

   Hence, the object became visible with the URL.

   ![Object Visible](https://github.com/user-attachments/assets/fd5f8e74-bc5e-4ac7-bf5a-6477440bf761)

In this case, I granted read access to just one specific object. If I wish to grant access to the entire bucket, I will need to use a bucket policy, which I will configure later.

## Objective - 4: Test Connectivity from the EC2 Instance

Now, I will connect to my Amazon Elastic Compute Cloud (Amazon EC2) instance to test connectivity and security with the S3 report bucket.

Session Manager enables us to connect to the bastion host instance without the need for specific ports to be open on the firewall or Amazon Virtual Private Cloud (Amazon VPC) security group.

![Session Manager](https://github.com/user-attachments/assets/cc66dc8a-8ef2-42a1-acdb-c6e1da8184d4)

Here, the output indicates an error: *upload failed*. This is because we have read-only rights to the bucket and do not have permission to perform the `PutObject` operation. I will create a bucket policy to grant `PutObject` permissions.

## Objective - 5: Create a Bucket Policy

A bucket policy is a set of permissions associated with an S3 bucket. It is used to control access to an entire bucket or specific directories within it.

Amazon Resource Names (ARNs) uniquely identify AWS resources. Each section of an ARN is separated by a colon `:` and represents a specific component in the path to the specified resource. The general format of an ARN is: arn:partition:service:region:account-id:resource

For Amazon S3, the `region` and `account-id` fields are optional, so the ARN for an S3 bucket looks like this: arn:aws:s3:::reportbucket987987

The `/*` at the end of the bucket name allows the policy to apply to all objects within the bucket.

### Steps Taken:

1. I generated a bucket policy using **AWS Policy Manager**, which looks like this:

   ![Bucket Policy](https://github.com/user-attachments/assets/a4c8bf66-e8ec-4fb4-a653-d2121462bde4)

2. I added the generated policy to the **Bucket Policy** section:

   ![Bucket Policy Section](https://github.com/user-attachments/assets/0930b908-f01b-422b-accd-817e73eaaab8)

3. To test the policy, I uploaded and retrieved a file from **EC2** to the S3 bucket.

   ![Test Upload](https://github.com/user-attachments/assets/aaf2f459-6933-41fe-933b-9663a9c6a8a0)

4. To ensure read access, I added another statement to the bucket policy allowing me to view the uploaded file:

   ![Added Policy Statement](https://github.com/user-attachments/assets/adabbe5f-22b6-4e08-83a9-a018876a4849)

5. After adding the statement, I successfully accessed the uploaded file, which no longer displayed an "Access Denied" error:

   ![Access Granted](https://github.com/user-attachments/assets/4a892561-538c-4425-9877-76ab190addb8)


## Objective - 6: Use Bucket Versioning

**Versioning** is a method of keeping multiple versions of an object in the same bucket. It allows me to recover from unintended user actions and application failures by preserving, retrieving, and restoring all versions of objects stored in the bucket.

### Steps Taken:

1. I enabled **Bucket Versioning** for my S3 bucket:

   ![Enable Versioning](https://github.com/user-attachments/assets/b5a677e4-5cad-4466-9d46-f3819fcfa5de)

2. With versioning enabled, all objects within the bucket can have multiple versions. Versioning cannot be enabled for individual objects—it applies to the entire bucket.

3. I updated the policy to include `s3:GetObjectVersion`, allowing me to retrieve specific object versions:

   ![Versioning Policy](https://github.com/user-attachments/assets/753112a0-7df4-4c2c-9d5a-0d71982ee499)

4. I tested the versioning feature by deleting an object from the bucket:

   ![Deleted Object](https://github.com/user-attachments/assets/eb1592c6-bd4a-447a-a86f-0cd953e94e8f)

5. After deleting the object, I enabled the version view. The deleted object appeared with a "delete marker," indicating that previous versions still exist:

   ![Delete Marker](https://github.com/user-attachments/assets/f447a602-63e8-41c0-bc4b-848dc080d622)

